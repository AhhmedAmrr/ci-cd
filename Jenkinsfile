pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('FIREBASE_TOKEN')
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Firebase Hosting') {
            steps {
                sh '''
                    apt-get update && apt-get install -y ca-certificates curl gnupg
                    mkdir -p /etc/apt/keyrings
                    curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
                    echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_20.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list
                    apt-get update && apt-get install nodejs -y
                    npm install -g firebase-tools@latest
                    firebase --version
                    firebase deploy --only hosting --token "$FIREBASE_TOKEN" --non-interactive
                '''
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}