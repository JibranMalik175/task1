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

        // ... your existing stages (Checkout, Install, Test, etc.)
    }

    post {
        success {
            echo "Build completed successfully at ${new Date()}"
        }
    }
}
