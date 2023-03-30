pipeline {
    agent {
        docker {
            image 'node:lts-bullseye-slim' 
            args '-p 33000:3000 -u 1000:1000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm config get cache'
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}