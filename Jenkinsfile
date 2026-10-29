pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Python application'
                sh 'python3 --version'
                sh 'pip3 --version'
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests'
                sh 'python3 -m unittest -v test_app'
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
