pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "flask-hello-navyseal"
        DOCKER_TAG = "latest"
        CONTAINER_NAME = "flask_app"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out repository...'
                git 'https://github.com/group-navyseal/sample-hello-navyseal.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker Image...'
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo 'Stopping old container (if exists)...'
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"

                    echo 'Running new container...'
                    sh "docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    echo 'Testing application availability...'
                    sh "curl -f http://localhost:5000 || exit 1"
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    echo 'Cleaning up old Docker images...'
                    sh "docker image prune -f"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
