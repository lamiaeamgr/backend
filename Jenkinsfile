pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "lamiaeamgr/backend:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'DevOpsTp', variable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u lamiaeamgr --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }
}
