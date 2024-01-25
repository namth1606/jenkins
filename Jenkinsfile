pipeline {
    agent any

    stages {
        stage('Stop image') {
            steps {
                sshagent(credentials: ['jenkins']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 uptime
                        docker stop wego-be || true && docker rm wego-be || true
                    '''
                }
            }
        }

        stage('Run new image') {
            steps {
                sshagent(credentials: ['jenkins']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no jenkins@35.209.7.50 uptime
                        docker run --name wego-be -d -p 8080:80 hoainam1606/we-be:1.0.20230903035453
                    '''
                }
            }
        }
    }
}
