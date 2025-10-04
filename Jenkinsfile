pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/ritesh355/docker-jenkins-app.git'
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
                    // Stop & remove if already running
                    sh 'docker stop docker-jenkins-app || true && docker rm docker-jenkins-app || true'
                    // Run new container
                    sh 'docker run -d --name docker-jenkins-app -p 3000:3000 docker-jenkins-app:latest'
                }
            }
        }
    }
}

