pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile.build'
            additionalBuildArgs '''\
            --build-arg GID=$(id -g) \
            --build-arg UID=$(id -u) \
            --build-arg UNAME=$(id -un) \
            '''
        }
    }
    stages {
        stage('Build') { 
            steps {
                script {
                    BUILD_TAG = "DEV-${env.BRANCH_NAME}-${env.GIT_BRANCH}-${params.BRANCH}"
                    echo "$BUILD_TAG"
                }
                // sh 'npm config get cache'
                // sh 'npm install' 
            }
        }
        // stage('Test') {
        //     steps {
        //         sh './jenkins/scripts/test.sh'
        //     }
        // }
        // stage('Deliver') {
        //     steps {
        //         sh './jenkins/scripts/deliver.sh'
        //         input message: 'Finished using the web site? (Click "Proceed" to continue)'
        //         sh './jenkins/scripts/kill.sh'
        //     }
        // }
    }
}