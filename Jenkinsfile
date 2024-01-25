pipeline {
    agent any

    stages {
        stage('Stop image') {
            steps {
                sshagent(credentials: ['jenkins']) {
                    sh '''
                        [ -d ~/.ssh ] || mkdir ~/.ssh && chmod 0700 ~/.ssh
                        ssh-keyscan -t rsa,dsa 35.209.7.50 >> ~/.ssh/known_hosts
                        ssh jenkins@35.209.7.50
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
                        [ -d ~/.ssh ] || mkdir ~/.ssh && chmod 0700 ~/.ssh
                        ssh-keyscan -t rsa,dsa 35.209.7.50 >> ~/.ssh/known_hosts
                        ssh jenkins@35.209.7.50
                        sudo su
                        docker run --name wego-be -d -p 8080:80 we-be:latest'
                    '''
                }
            }
        }
    }
}
