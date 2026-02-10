pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                dir('app') {
                    bat 'npm install'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                dir('app') {
                    bat 'docker build -t nodejs-app .'
                }
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
}
