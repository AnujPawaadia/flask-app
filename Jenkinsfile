pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
        IMAGE_NAME = 'anujpawadia0125/flask-app:latest'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AnujPawaadia/flask-app'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.IMAGE_NAME)
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    def image = docker.image(env.IMAGE_NAME)
                    docker.withRegistry('https://index.docker.io/v1/', env.DOCKERHUB_CREDENTIALS) {
                        image.push()
                    }
                }
            }
        }
        stage('Deploy to Minikube') {
            steps {
                echo '⚠️ Minikube deployment must be done manually. Run locally:'
                echo 'kubectl apply -f deployment.yaml'
                echo 'kubectl apply -f service.yaml'
                echo 'kubectl wait --for=condition=ready pod -l app=flask-app --timeout=60s'
            }
        }
    }
}
