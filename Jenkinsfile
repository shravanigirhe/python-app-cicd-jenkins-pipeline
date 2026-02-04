pipeline {
    agent any

    environment {
        PYTHON = 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python312\\python.exe'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Check Python Version') {
            steps {
                bat "\"%PYTHON%\" --version"
            }
        }

        stage('Create Virtual Environment') {
            steps {
                bat "\"%PYTHON%\" -m venv venv"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                venv\\Scripts\\activate
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                venv\\Scripts\\activate
                pytest
                '''
            }
        }
    }

    post {
        success {
            echo '✅ CI Pipeline SUCCESS'
        }
        failure {
            echo '❌ CI Pipeline FAILED'
        }
    }
}
