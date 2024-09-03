pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                git branch: 'main', url: 'https://github.com/khrlvlnc/node-webapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image from the Dockerfile
                script {
                    docker.build('node-webapp-image')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the Docker container using the built image
                script {
                    docker.image('node-webapp-image').run('-d -p 8080:8080')
                }
            }
        }
    }
}

