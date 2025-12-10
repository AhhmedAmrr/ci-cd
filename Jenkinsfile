
pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token') 
        NETLIFY_SITE_ID = '1a26b4da-5a94-4e34-9575-1a39797d37f5'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/AhhmedAmrr/ci-cd.git', branch: 'main'
            }
        }

        stage('Deploy to Netlify') {
            steps {
                echo "Deploying site to Netlify using Docker..."
                sh '''
                docker run --rm \
                  -v $PWD:/app \
                  -w /app \
                  -e NETLIFY_AUTH_TOKEN=$NETLIFY_AUTH_TOKEN \
                  -e NETLIFY_SITE_ID=$NETLIFY_SITE_ID \
                  netlify/cli deploy --dir /app --prod --site $NETLIFY_SITE_ID --auth $NETLIFY_AUTH_TOKEN --message "Deployed by Jenkins"
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment succeeded ✅"
        }
        failure {
            echo "Deployment failed ❌"
        }
    }
}
