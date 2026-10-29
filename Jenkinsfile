
pipeline {
    agent any

    environment {
        PYTHON = "C:\\Users\\Piyusha\\AppData\\Local\\Programs\\Python\\Python311\\python.exe"
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '"%PYTHON%" -m venv .venv'
                bat '".venv\\Scripts\\python.exe" -m pip install --upgrade pip'
                bat '".venv\\Scripts\\python.exe" -m pip install -r requirements.txt'
            }
        }

        stage('Run Application') {
            steps {
                bat '".venv\\Scripts\\python.exe" hello.py'
            }
        }

        stage('Run pytest') {
            steps {
                bat '".venv\\Scripts\\python.exe" -m pytest -v'
            }
        }

        stage('Evidently Monitoring') {
            steps {
                bat '".venv\\Scripts\\python.exe" monitor.py'
            }
        }
    }

    post {
        always {
            archiveArtifacts(
                artifacts: 'evidently_report.html',
                allowEmptyArchive: true
            )
        }
    }
}
