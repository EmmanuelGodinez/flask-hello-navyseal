pipeline {
    agent any
    
    environment {
        GIT_REPO_URL = 'git@github.com:EmmanuelGodinez/flask-hello-navyseal.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out repository..."
                checkout scm: [
                    $class: 'GitSCM',
                    branches: [[name: "*/${BRANCH}"]],
                    extensions: [],
                    userRemoteConfigs: [[url: GIT_REPO_URL]]
                ]
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running Docker container...'
            }
        }

        stage('Test Application') {
            steps {
                echo 'Testing application...'
            }
        }

        stage('Clean Up') {
            steps {
                echo 'Cleaning up...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
