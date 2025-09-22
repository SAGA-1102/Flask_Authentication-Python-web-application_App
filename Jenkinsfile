pipeline {
    agent any

    environment {
        PYTHON_ENV = 'venv'
    }

    stages {
        stage('Build') {
            steps {
                sh 'python -m venv $PYTHON_ENV'
                sh '$PYTHON_ENV\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh '$PYTHON_ENV\\Scripts\\pytest tests/'
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
            mail to: 'your-email@example.com',
                 subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build passed and deployed."
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed. Check Jenkins logs."
        }
    }
}
