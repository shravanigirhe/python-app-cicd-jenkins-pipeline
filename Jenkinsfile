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
                sh '''
                python3 --version
                python3 -m venv venv
                venv/bin/python -m pip install --upgrade pip
                venv/bin/python -m pip install pytest pytest-html pytest-cov
                '''
            }
        }

        stage('Verify Pytest') {
            steps {
                sh '''
                venv/bin/python -m pytest --version
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                venv/bin/python -m pytest --html=report.html --self-contained-html
                '''
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
