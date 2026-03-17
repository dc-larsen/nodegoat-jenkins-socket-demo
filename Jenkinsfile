pipeline {
    agent any

    environment {
        SOCKET_SECURITY_API_TOKEN = credentials('socket-api-key')
        REPO_NAME = "${env.REPO_NAME ?: 'nodegoat-jenkins-socket-demo'}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install --production'
            }
        }

        stage('Socket Security Scan') {
            steps {
                sh """
                    socketcli \
                        --target-path . \
                        --repo ${env.REPO_NAME ?: 'nodegoat-jenkins-socket-demo'} \
                        --default-branch \
                        --reach \
                        --reach-ecosystems npm \
                        --disable-blocking \
                        --integration api
                """
            }
        }
    }

    post {
        always {
            echo 'Scan complete. View results at https://socket.dev/dashboard'
        }
    }
}
