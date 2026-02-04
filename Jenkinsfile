pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo '📥 Cloning GitHub repository'
                checkout scm
            }pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo '📥 Cloning GitHub repository'
                checkout scm
            }
        }

        stage('Check Python Version') {
            steps {
                bat 'py --version'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                bat 'py -m venv venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                venv\\Scripts\\activate
                py -m pip install --upgrade pip
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
            echo '✅ CI Pipeline completed successfully!'
        }
        failure {
            echo '❌ CI Pipeline failed. Check logs.'
        }
    }
}

        }

        stage('Check Python Version') {
            steps {
                bat 'python --version'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                bat '''
                python -m venv venv
                '''
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
            echo '✅ CI Pipeline completed successfully!'
        }
        failure {
            echo '❌ CI Pipeline failed. Check logs.'
        }
    }
}

