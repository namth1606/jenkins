pipeline {
    agent any

    stages {
        stage('SSH to Server') {
            steps {
                sshagent(['jenkins']) {
                    sh "ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 'docker stop wego-be || true && docker rm wego-be || true'" // Stop and remove any existing container
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                sshagent(['jenkins']) {
                    sh "ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 'docker run -d -p 8080:80 we-be:latest'" // Replace with your desired docker run command
                }
            }
        }
    }
}
