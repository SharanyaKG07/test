pipeline {
    agent any

    environment {
        
        DOCKER_REPO = "sharanya0705/app-image"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                
                bat 'docker build -t %DOCKER_REPO%:latest .'
            }
        }

        stage('Login and Push') {
            steps {
                script {
                    
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds2') {
                        docker.image("${DOCKER_REPO}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline Success: Image pushed to Docker Hub'
        }
        failure {
            echo 'Pipeline Failed: Check credentials or Docker Hub status'
        }
    }
}