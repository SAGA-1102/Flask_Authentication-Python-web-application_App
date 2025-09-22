pipeline {
    agent any

    environment {
        PYTHON_ENV = 'venv'
    }

    stages {
        stage('Build') {
            steps {
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'venv\\Scripts\\pytest tests'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying to staging...'
                // Add deployment logic here
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
            // Optional: add email logic once SMTP is configured
        }
        failure {
            echo 'Build failed!'
            // Optional: add email logic once SMTP is configured
        }
    }
}
