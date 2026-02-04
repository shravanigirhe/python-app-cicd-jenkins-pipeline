pipeline {
    agent any

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
                venv\\Scripts\\python -m pip install --upgrade pip
                venv\\Scripts\\python -m pip install -r requirements.txt
                venv\\Scripts\\python -m pip install pytest pytest-html pytest-cov
                """
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                bat """
                venv\\Scripts\\python -m pytest --html=report.html --self-contained-html
                """
            }
        }

    }

    post {
        always {
            echo 'Pipeline completed'
            archiveArtifacts artifacts: 'report.html', fingerprint: true
        }
    }
}
