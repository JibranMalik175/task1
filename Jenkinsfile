pipeline {
    agent any

    triggers {
        githubPush() // Automatically triggered by GitHub Webhook
    }

    environment {
        APP_NAME = "nodeapp"
        DEPLOY_DIR = "C:\\pm2deploy\\nodeapp" // Change this if needed
    }

    stages {
        stage('Build Info') {
            steps {
                script {
                    echo "🚀 Build #${env.BUILD_NUMBER} started at ${new Date()}"
                    def causes = currentBuild.rawBuild.getCauses()
                    if (causes.toString().contains("GitHub")) {
                        echo "Triggered by GitHub Webhook"
                    } else {
                        echo "Manually triggered build"
                    }
                }
            }
        }

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

        stage('Test') {
            steps {
                bat 'npm test || echo "No tests found"'
            }
        }

        stage('Build & Package') {
            steps {
                bat 'tar -a -c -f build-output.zip *'
                archiveArtifacts artifacts: 'build-output.zip', fingerprint: true
            }
        }

        stage('Deploy with PM2') {
            steps {
                script {
                    echo "🛠️ Deploying app using PM2..."
                    // Ensure deployment directory exists
                    bat """
                    if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                    xcopy * "%DEPLOY_DIR%" /E /Y
                    cd "%DEPLOY_DIR%"
                    pm2 delete %APP_NAME% || echo "No previous instance found"
                    pm2 start server.js --name %APP_NAME%
                    pm2 save
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment completed successfully at ${new Date()}"
        }
        failure {
            echo "❌ Deployment failed! Check Jenkins logs for errors."
        }
    }
}
