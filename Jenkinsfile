pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'rajyjay/jenkins-node-app'
        DOCKER_USERNAME = 'rajyjay'
        DOCKER_PASSWORD = 'yourActualPasswordHere' // 🔁 Replace this with your actual Docker Hub password or token
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-repo/jenkins-node-app.git' // 🔁 Replace with your actual Git repo URL
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm install'
                bat 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }

        stage('Push Docker Image') {
            steps {
                bat """
                    echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
                    docker push %DOCKER_IMAGE%
                """
            }
        }
    }
}

