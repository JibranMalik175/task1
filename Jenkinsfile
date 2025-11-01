pipeline {
    agent any

    environment {
        PM2_HOME = "C:\\Users\\Jibran Malik\\.pm2"
        NODE_ENV = "production"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/JibranMalik175/task1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Restart App with PM2') {
            steps {
                bat '''
                pm2 delete task1 || echo "No previous instance found"
                pm2 start server.js --name task1
                pm2 save
                pm2 list
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! App restarted via PM2."
        }
        failure {
            echo "❌ Deployment failed. Check Jenkins logs."
        }
    }
}
