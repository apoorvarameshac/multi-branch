pipeline {
    agent any

    environment {
        IMAGE_NAME = "apoorvar12/dev-java-app"
        IMAGE_TAG = "dev-${BUILD_NUMBER}"
        FULL_IMAGE = "${IMAGE_NAME}:${IMAGE_TAG}"
        CONTAINER_NAME = "dev-container"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'dev', credentialsId: 'github', url: 'https://github.com/apoorvarameshac/multi-branch.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build --no-cache -t $FULL_IMAGE .'
            }
        }

        stage('Create Container') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME -p 8082:8080 $FULL_IMAGE
                '''
            }
        }
    }
}

