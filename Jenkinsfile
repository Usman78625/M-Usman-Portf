pipeline {
    agent any

    tools {
        nodejs "Node"
    }

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-auth-token')  // Store your Netlify auth token as a Jenkins credential
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking Git ...'
                git branch: 'testing', url: 'https://github.com/Usman78625/M-Usman-Portf.git'
                echo 'Done'
            }
        }
        
        stage("Install Dependencies") {
            steps {
                sh 'npm install -g @angular/cli@13.2.3'
                sh 'npm install --force'
                sh 'npm install -g netlify-cli'

            }
        }
        
        stage('Build') {
            steps {
                // Build the Angular project
                sh 'npm run build --prod'
            }
        }
        
        stage('Deploy to Netlify') {
            steps {
                echo 'Deploying to Netlify...'
                withEnv(["NETLIFY_AUTH_TOKEN=${env.NETLIFY_AUTH_TOKEN}"]) {
                    // Replace 'your-site-id' with your actual Netlify site ID
                    sh 'npx netlify deploy --prod --dir=dist/M.Usman-portfolio --site=b144f0bf-f20d-494d-9703-c976b4fadf1a'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
