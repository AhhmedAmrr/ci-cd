pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('FIREBASE_TOKEN')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Firebase Tools') {
            steps {
                sh 'npm install -g firebase-tools'
            }
        }

        stage('Deploy to Firebase') {
            steps {
                sh "firebase deploy --token $FIREBASE_TOKEN"
            }
        }
    }
}