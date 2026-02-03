pipeline {
    agent any
    tools {
        // Optional: If you have Python configured in Jenkins Global Tools
        // python 'Python3'
    }
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
        stage('Build / Compile Check') {
            steps {
                echo 'Checking Python syntax...'
                bat """
                venv\\Scripts\\activate
                python -m py_compile app.py
                """
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Running unit tests with pytest...'
                bat """
                venv\\Scripts\\activate
                pytest test.py --junitxml=test-reports\\results.xml --html=test-reports\\report.html --self-contained-html
                """
            }
            post {
                always {
                    echo 'Archiving test results...'
                    junit 'test-reports\\results.xml'
                    publishHTML(target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'test-reports',
                        reportFiles: 'report.html',
                        reportName: 'Pytest HTML Report'
                    ])
                }
            }
        }
    }
    post {
        success {
            echo 'Python CI Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the test results.'
        }
    }
}
