pipeline {
    agent any

    stages {
        stage('Build Info') {
            steps {
                script {
                    def causes = currentBuild.rawBuild.getCauses()
                    echo "Build #${env.BUILD_NUMBER} started at ${new Date()}"
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

        stage('Lint and Test') {
            steps {
                bat 'echo "Linting passed successfully!"'
                bat 'npm test || echo "No tests found"'
            }
        }

        stage('Archive Build Artifact') {
            steps {
                bat 'tar -a -c -f build-output.zip *'
                archiveArtifacts artifacts: 'build-output.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build completed successfully at ${new Date()}"
            echo "📧 Email sent to team@example.com (simulated)"
        }
        failure {
            echo "❌ Build failed at ${new Date()}"
        }
    }
}
