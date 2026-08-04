pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('jenkins-local-to-docker-hub')
        IMAGE_NAME = 'vopula/vopula_owaspjuiceshop'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }
    }
    
    post {
        always {
            sh 'docker logout'
        }
    }
}