pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "anoop10/node_app"
        DOCKER_CREDENTIALS_ID = "dockerhub"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/bohemliving/SampleNodeApp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image pushed successfully!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
