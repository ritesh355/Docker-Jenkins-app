pipeline {
    agent any

    environment {
        HOST_PORT = '4000'  // Change if needed, or pass dynamically
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/ritesh355/Docker-Jenkins-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t docker-jenkins-app:latest .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop & remove old container if exists
                    sh 'docker stop docker-jenkins-app || true && docker rm docker-jenkins-app || true'
                    // Run new container with dynamic host port
                    sh "docker run -d --name docker-jenkins-app -p ${HOST_PORT}:3000 docker-jenkins-app:latest"
                }
            }
        }
    }
}
