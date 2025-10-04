pipeline {
    agent any

    environment {
        HOST_PORT = '4000'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/ritesh355/Docker-Jenkins-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t docker-jenkins-app:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker stop docker-jenkins-app || true && docker rm docker-jenkins-app || true'
                sh "docker run -d --name docker-jenkins-app -p ${HOST_PORT}:3000 docker-jenkins-app:latest"
            }
        }
    }

    post {
        success {
            emailext(
                subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Good news! Build ${env.BUILD_NUMBER} succeeded.\nCheck details: ${env.BUILD_URL}",
                to: "riteshsingh86991@gmail.com"
            )
        }
        failure {
            emailext(
                subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Oops! Build ${env.BUILD_NUMBER} failed.\nCheck details: ${env.BUILD_URL}",
                to: "riteshsingh86991@gmail.com"
            )
        }
    }
}

