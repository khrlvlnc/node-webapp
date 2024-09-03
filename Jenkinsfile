pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Build Podman Image') {
            steps {
                script {
                    // Build the container image using podman
                    sh 'podman build -t node-webapp-image .'
                }
            }
        }

        stage('Run Podman Container') {
            steps {
                script {
                    // Run the container using podman
                    sh 'podman run -d --name node-webapp-container -p 8080:8080 node-webapp-image'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Test the running container (replace with your actual test commands)
                    sh 'curl http://localhost:8080'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Stop and remove the container, and optionally remove the image
                    sh 'podman stop node-webapp-container'
                    sh 'podman rm node-webapp-container'
                    // Optionally remove the image
                    // sh 'podman rmi node-webapp-image'
                }
            }
        }
    }
    
    post {
        always {
            // Archive the build artifacts or perform other post-build actions
            // For example, you might archive test results or build reports
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}

