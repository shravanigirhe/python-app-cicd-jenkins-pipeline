pipeline {
    agent any
    // Remove the tools block completely
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }
        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python virtual environment...'
                bat """
                python -m venv venv
                venv\\Scripts\\activate
                pip install --upgrade pip
                pip install -r requirements.txt
                pip install pytest pytest-html pytest-cov
                """
            }
        }
        ...
