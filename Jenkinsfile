pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat '''
                python --version
                python -m venv venv
                call venv\\Scripts\\activate
                python -m pip install --upgrade pip
                python -m pip install -r requirements.txt
                python -m pip install pytest pytest-html pytest-cov
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                python -m pytest
                '''
            }
        }
    }
}
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat """
                python --version
                python -m venv venv
                venv\\Scripts\\python -m pip install --upgrade pip
                venv\\Scripts\\python -m pip install pytest pytest-html pytest-cov
                """
            }
        }

        stage('Verify Pytest') {
            steps {
                bat """
                venv\\Scripts\\python -m pytest --version
                """
            }
        }

        stage('Run Tests') {
            steps {
                bat """
                venv\\Scripts\\python -m pytest --html=report.html --self-contained-html
                """
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'report.html', fingerprint: true
        }
    }
}

