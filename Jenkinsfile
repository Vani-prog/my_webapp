 pipeline {
    agent any

    // triggers {
    //     cron('* * * * *')   // runs every minute
    // }

    environment {
        DOCKERHUB_CRED = credentials('dockerhub')
        IMAGE_NAME = "vanireddy2025/my_webapp"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Vani-prog/my_webapp.git',
                    branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Docker image built and pushed successfully"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
