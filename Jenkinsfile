pipeline {
    environment {
        JENKINS_USER_NAME = "${sh(script:'id -un', returnStdout: true).trim()}"
        JENKINS_USER_ID = "${sh(script:'id -u', returnStdout: true).trim()}"
        JENKINS_GROUP_ID = "${sh(script:'id -g', returnStdout: true).trim()}"
    }
    agent {
        dockerfile {
            filename 'Dockerfile.build'
            additionalBuildArgs '''\
            --build-arg GID=$JENKINS_GROUP_ID \
            --build-arg UID=$JENKINS_USER_ID \
            --build-arg UNAME=$JENKINS_USER_NAME \
            '''
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