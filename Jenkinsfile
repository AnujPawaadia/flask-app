pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AnujPawaadia/flask-app'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('anujpawadia0125/flask-app:latest')
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Use the correct credential ID 'docker-password'
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-password') {
                        docker.image('anujpawadia0125/flask-app:latest').push()
                    }
                }
            }
        }

        stage('Deploy to Minikube') {
            steps {
                echo 'Minikube deployment is manual. Run locally:'
                echo 'kubectl apply -f deployment.yaml'
                echo 'kubectl apply -f service.yaml'
                echo 'kubectl wait --for=condition=ready pod -l app=flask-app --timeout=60s'
            }
        }
    }
}
