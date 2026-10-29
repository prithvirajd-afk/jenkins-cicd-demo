pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Python application'
                sh '''
                    python3 --version
                    python3 -m venv .venv
                    .venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests'
                sh '.venv/bin/python -m unittest -v test_app'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Build and tests completed successfully'
                echo 'Docker deployment will be configured next'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
