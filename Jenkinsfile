
pipeline {
    agent any

    stages {
        stage('Setup') {
            steps {
                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    .venv/bin/python -m pytest -v --junitxml=results.xml || true
                '''
            }
        }
    }

    post {
        always {
            junit 'results.xml'
        }
    }
}
