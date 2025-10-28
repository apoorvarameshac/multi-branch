pipeline {
    agent any

    environment {
        IMAGE_NAME = "apoorvar12/prod-java-app"
        IMAGE_TAG = "prod-${BUILD_NUMBER}"
        FULL_IMAGE = "${IMAGE_NAME}:${IMAGE_TAG}"
        CONTAINER_NAME = "prod-container"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/apoorvarameshac/multi-branch.git'
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
                    docker run -d --name $CONTAINER_NAME -p 8081:8080 $FULL_IMAGE
                '''
            }
        }
    }
}

