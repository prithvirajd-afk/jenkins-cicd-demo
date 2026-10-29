
pipeline {
    agent any

    environment {
        DOCKER_HOST = 'tcp://docker-daemon:2375'
        IMAGE_NAME = 'jenkins-cicd-demo:latest'
        CONTAINER_NAME = 'jenkins-cicd-app'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Python application'
                sh '''
                    python3 --version
                    python3 -m venv .venv
                    .venv/bin/pip install -r requirements.txt
                    docker build -t $IMAGE_NAME .
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
                echo 'Deploying application with Docker'
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d \
                        --name $CONTAINER_NAME \
                        --restart unless-stopped \
                        -p 5000:5000 \
                        $IMAGE_NAME
                '''
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
