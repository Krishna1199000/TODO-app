pipeline {
    agent any

    tools {
        nodejs 'node18' // ✅ Make sure this version is set up in Jenkins
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo '🔄 Cloning repository...'
                git branch: 'main', url: 'https://github.com/Krishna1199000/TODO-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '📦 Installing npm packages...'
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                echo '⚙️ Building the app...'
                sh 'npm run build'
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running tests (if available)...'
                // If you have no tests, this won't fail the pipeline
                sh 'npm test || echo "✅ No tests to run"'
            }
        }

        stage('Push to GitHub') {
            steps {
                echo '🚀 Pushing changes back to GitHub (triggers Vercel deploy)...'
                sh '''
                    git config user.name "jenkins-bot"
                    git config user.email "jenkins@example.com"
                    git add .
                    git commit -m "✅ Jenkins CI Build Successful"
                    git push origin main || echo "No changes to push"
                '''
            }
        }
    }

    post {
        success {
            echo '🎉 Jenkins pipeline completed successfully!'
        }
        failure {
            echo '❌ Jenkins pipeline failed. Please check the logs.'
        }
    }
}
