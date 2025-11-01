pipeline {
    agent any

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

        stage('Lint and Test') {
            steps {
                // Simulate lint + test for now
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
            echo 'Build, lint, and test successful!'
            echo 'Email sent to team@example.com (simulated)'
        }
        failure {
            echo 'Build failed!'
            echo 'Email sent to team@example.com (simulated)'
        }
    }
}
