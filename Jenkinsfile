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
            echo 'Deployment to Firebase Hosting succeeded!'
        }
        failure {
            echo 'Deployment failed. Check the logs.'
        }
    }
}