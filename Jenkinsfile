pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Dhishanthdgp123/cicd.git'
            }
        }
        stage('Copy to Docker Host') {
            steps {
                sh 'scp -i ~/.ssh/cicd -o StrictHostKeyChecking=no -r * ubuntu@3.108.64.4:/home/ubuntu/app'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'ssh -i ~/.ssh/cicd -o StrictHostKeyChecking=no ubuntu@3.108.64.4 "cd /home/ubuntu/app && docker build -t frontend-app ."'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'ssh -i ~/.ssh/cicd -o StrictHostKeyChecking=no ubuntu@3.108.64.4 "docker rm -f frontend-app || true && docker run -d -p 80:80 --name frontend-app frontend-app"'
            }
        }
    }
}
