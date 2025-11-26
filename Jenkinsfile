pipeline {
    agent any

    environment {
        // CHANGE if you used different credential ID (only needed for private repo)
        GIT_CREDENTIALS = '' // leave empty for public repo; or set 'github-ssh' or 'github-pat'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository from GitHub..."
                // If the repo is public, this will work without credentials:
                git branch: 'main',
                    url: 'https://github.com/meghanap05/GitEx.git',
                    credentialsId: "${GIT_CREDENTIALS}"
            }
        }

        stage('Build') {
            steps {
                echo "Building with Maven: mvn clean package"
                sh 'mvn -B clean package'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running unit tests: mvn test"
                sh 'mvn -B test'
            }
            post {
                always {
                    echo "Publishing JUnit test results to Jenkins"
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive') {
            steps {
                echo "Archiving built artifacts (.jar/.war) from target/"
                archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "SUCCESS: Build and tests passed!"
        }
        failure {
            echo "FAILURE: Build or tests failed — check console and test report."
        }
        always {
            echo "Pipeline finished — check console output and test reports."
        }
    }
}
