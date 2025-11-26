pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository from GitHub..."
                git branch: 'main', url: 'https://github.com/meghanap05/GitEx.git'
            }
        }

        stage('Build') {
            steps {
                echo "Simulating build..."
                bat 'echo Build successful!'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Simulating tests..."
                bat 'echo Tests passed!'
            }
        }

        stage('Archive') {
            steps {
                echo "Simulating artifact archive..."
                bat 'echo Artifacts archived!'
            }
        }
    }

    post {
        success {
            echo "BUILD SUCCESS 🎉"
        }
        failure {
            echo "BUILD FAILED ❌"
        }
        always {
            echo "Pipeline finished."
        }
    }
}
