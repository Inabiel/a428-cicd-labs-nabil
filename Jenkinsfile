// node{
//     docker.image('node:lts-bullseye-slim').inside('-p 3000:3000'){
//         stage('Build') { 
//                 echo "test test test"
//                 sh 'npm install' 
//         }
//          stage('Test') {
//                 sh './jenkins/scripts/test.sh'
//         }
//     }  
// }

pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}