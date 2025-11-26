pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning repository from GitHub..."
                git branch: 'main',
                    url: 'https://github.com/meghanap05/GitEx.git'
            }
        }

        stage('Build') {
            steps {
                echo "Running Maven build..."
                bat 'mvn -B clean package'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running tests..."
                bat 'mvn -B test'
            }
            post {
                always {
                    echo "Publishing test results..."
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive') {
            steps {
                echo "Archiving build artifacts..."
                archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true
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
