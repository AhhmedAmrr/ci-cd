pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'your-site-id-here'          
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')      }

    stages {
        stage('Deploy to Netlify using Jenkins') {
            steps {
                sh '''
                    echo "Jenkins is deploying your static site to Netlify..."
                    npx netlify-cli deploy --dir . --prod --site $NETLIFY_SITE_ID --auth $NETLIFY_AUTH_TOKEN --message "Deployed by Jenkins - Task Done ✓"
                '''
            }
        }
    }

    post {
        success {
            echo 'Deloy done'
        }
        failure {
            echo 'error'
        }
    }
}