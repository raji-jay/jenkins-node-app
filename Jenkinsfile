pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'rajyjay/jenkins-node-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-user/jenkins-node-app.git'
            }
        }

        stage('Test') {
            steps {
                bat 'npm install'
                bat 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat 'echo %PASSWORD% | docker login -u %USERNAME% --password-stdin'
                    bat 'docker push %DOCKER_IMAGE%'
                }
            }
        }
    }
}
