pipeline {
    agent any

    environment {
         NETLIFY_AUTH_TOKEN = credentials('netlify-token') 
        NETLIFY_SITE_ID = '1a26b4da-5a94-4e34-9575-1a39797d37f5'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Netlify CLI') {
            steps {
                bat 'npm install -g netlify-cli'
            }
        }

        stage('Deploy to Netlify') {
            steps {
                bat """
                    netlify deploy --prod ^
                    --auth "%NETLIFY_TOKEN%" ^
                    --dir=.
                """
            }
        }
    }
}