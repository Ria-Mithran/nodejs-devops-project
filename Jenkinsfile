pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                // We removed dir('app') because package.json is in the root now
                bat 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                // We removed dir('app') because Dockerfile is in the root now
                bat 'docker build -t nodejs-app .'
            }
        }
        stage('Run Container') {
            steps {
                bat '''
                    docker rm -f nodejs-app || exit 0
                    docker run -d -p 3000:3000 --name nodejs-app nodejs-app
                '''
            }
        }
    }
