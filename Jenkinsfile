pipeline {
    agent any

    stages {
        stage('Stop image') {
            steps {
                sshagent(credentials: ['jenkins']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50
                        sudo su
                        docker stop wego-be || true && docker rm wego-be || true
                    '''
                }
            }
        }

        stage('Run new image') {
            steps {
                sshagent(credentials: ['jenkins']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50
                        sudo su
                        docker run --name wego-be -d -p 8080:80 we-be:latest'
                    '''
                }
            }
        }
    }
}
