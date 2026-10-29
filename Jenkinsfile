
pipeline {
    agent any

    stages {
        stage('Checkout from GitHub') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Run Application') {
            steps {
                bat 'python hello.py'
            }
        }

        stage('Run pytest') {
            steps {
                bat 'python -m pytest -v'
            }
        }

        stage('Evidently Monitoring') {
            steps {
                bat 'python monitor.py'
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
