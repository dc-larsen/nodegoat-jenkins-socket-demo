pipeline {
    agent any

    environment {
        SOCKET_SECURITY_API_TOKEN = credentials('socket-api-key')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Socket Security Scan') {
            steps {
                sh '''
                    socketcli \
                        --target-path . \
                        --repo dc-larsen/nodegoat-jenkins-socket-demo \
                        --default-branch \
                        --reach \
                        --reach-ecosystems npm \
                        --disable-blocking \
                        --integration api
                '''
            }
        }
    }

    post {
        always {
            echo 'Scan complete. View results at https://socket.dev/dashboard'
        }
    }
}
