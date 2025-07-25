pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Dhishanthdgp123/cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'scp -i ~/.ssh/cicd.pem -o StrictHostKeyChecking=no -r * ubuntu@3.108.64.4:/home/ubuntu/app'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                ssh -i ~/.ssh/cicd.pem -o StrictHostKeyChecking=no ubuntu@3.108.64.4 << EOF
                  cd /home/ubuntu/app
                  echo -e 'FROM nginx\\nCOPY . /usr/share/nginx/html' > Dockerfile
                  docker build -t frontend-image .
                  docker run -d -p 80:80 frontend-image
                EOF
                '''
            }
        }
    }
}
