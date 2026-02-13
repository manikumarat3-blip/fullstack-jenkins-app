pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend:latest backend/'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t frontend:latest frontend/'
            }
        }

        stage('Run Containers') {
            steps {
                sh '''
                docker stop backend || true
                docker rm backend || true
                docker run -d -p 5000:5000 --name backend backend:latest

                docker stop frontend || true
                docker rm frontend || true
                docker run -d -p 3000:3000 --name frontend frontend:latest
                '''
            }
        }
    }
}
