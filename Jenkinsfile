pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python310\\python.exe" -m venv venv'
                bat 'venv\\Scripts\\pip.exe install -r requirements.txt'
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
            mail to: 'your-email@gmail.com',
                 subject: "✅ Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Hello Sanidhya,

Your Jenkins build for '${env.JOB_NAME}' completed successfully.

Build Number: ${env.BUILD_NUMBER}
Status: SUCCESS
URL: ${env.BUILD_URL}

Cheers,
Jenkins"""
        }
        failure {
            mail to: 'your-email@gmail.com',
                 subject: "❌ Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Hello Sanidhya,

Your Jenkins build for '${env.JOB_NAME}' has failed.

Build Number: ${env.BUILD_NUMBER}
Status: FAILURE
URL: ${env.BUILD_URL}

Please check the logs and fix the issue.

Regards,
Jenkins"""
        }
    }
}
