
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
                script {
                    int exitCode = sh(
                        script: '.venv/bin/python -m pytest -v --junitxml=results.xml',
                        returnStatus: true
                    )

                    if (exitCode == 1) {
                        unstable('Some pytest tests failed')
                    } else if (exitCode != 0) {
                        error("pytest execution failed with exit code ${exitCode}")
                    }
                }
            }
        }
    }

    post {
        always {
            junit 'results.xml'
        }
    }
}
