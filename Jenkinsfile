pipeline {
    agent any

    environment {
        BACKEND_IMAGE = 'anujp4061/wanderlust-backend:latest'
        FRONTEND_IMAGE = 'anujp4061/wanderlust-frontend:latest'
        DOCKERHUB_CREDENTIALS = 'dockerHub-creds'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    docker.build(BACKEND_IMAGE, "./backend")
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                script {
                    docker.build(FRONTEND_IMAGE, "./frontend")
                }
            }
        }

        stage('Push Images to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        docker.image(BACKEND_IMAGE).push()
                        docker.image(FRONTEND_IMAGE).push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker images built and pushed successfully 🚀'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}