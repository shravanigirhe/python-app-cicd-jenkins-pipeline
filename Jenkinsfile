pipeline {
    agent any

    environment {
        PYTHON = 'python3'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Check Python Version') {
            steps {
                sh "$PYTHON --version"
            }
        }

        stage('Create Virtual Environment') {
            steps {
                sh "$PYTHON -m venv venv"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                source venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source venv/bin/activate
                pytest
                '''
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline SUCCESS'
        }
        failure {
            echo 'CI Pipeline FAILED'
        }
    }
}
