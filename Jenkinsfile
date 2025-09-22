pipeline {
    agent any

    stages {
        stage('Verify Python') {
            steps {
                bat 'where python'
            }
        }

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
            steps {
                echo 'Deploying to staging...'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
