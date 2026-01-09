pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'vitalikergin/flask-hello-world'
        DOCKER_TAG = "${env.BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from Git...'
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image: ${DOCKER_IMAGE}:${DOCKER_TAG}"
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                    sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest"
                }
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running tests - Verifying Docker image was created...'
                script {
                    sh "docker images | grep ${DOCKER_IMAGE}"
                }
            }
        }
        
        stage('Deploy to Minikube') {
            steps {
                echo 'Deploying to Minikube using Helm...'
                script {
                    sh """
                        helm upgrade --install flask-app ./kubernetes/flask-app \
                        --set image.repository=${DOCKER_IMAGE} \
                        --set image.tag=${DOCKER_TAG} \
                        --wait
                    """
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully! ✅'
        }
        failure {
            echo 'Pipeline failed! ❌'
        }
    }
}
