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
                    curl -L https://firebase.tools/bin/linux/x64/firebase -o firebase
                    chmod +x firebase
                    ./firebase --version
                    ./firebase deploy --only hosting --token $FIREBASE_TOKEN --non-interactive
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment to Firebase Hosting succeeded!'
        }
        failure {
            echo 'Deployment failed. Check the logs.'
        }
        always {
            cleanWs()
        }
    }
}