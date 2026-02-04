pipeline {
    agent {
        docker {
            image 'python:3.12'
        }
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                python --version
                python -m venv venv
                venv/bin/python -m pip install --upgrade pip
                venv/bin/python -m pip install pytest pytest-html pytest-cov
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
            archiveArtifacts artifacts: 'report.html', fingerprint: true
        }
    }
}
