pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'satyammay/sample-dev'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Use 'npm install' in a Windows batch script
                bat 'npm install'
            }
        }



        stage('Build Docker Image') {
            steps {
                // Build the Docker image using Docker CLI
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry(credentialsId: 'docker-hub-id', url: 'https://index.docker.io/v1/') {
                    bat "docker push %DOCKER_IMAGE%"
                }
            }
        }
    }

    post {
        success {
            echo 'Build and push successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
