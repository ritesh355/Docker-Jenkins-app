pipeline {
    agent any

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
                    // Stop & remove old container if running
                    sh 'docker stop docker-jenkins-app || true && docker rm docker-jenkins-app || true'
                    // Run new container on port 4000
                    sh 'docker run -d --name docker-jenkins-app -p 4000:3000 docker-jenkins-app:latest'
                }
            }
        }
    }
}
