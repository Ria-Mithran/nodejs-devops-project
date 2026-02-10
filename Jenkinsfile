pipeline {
    agent any
    environment {
        // This is the ID you will create in Jenkins Credentials
        DOCKER_HUB_USER = 'your-dockerhub-username'
    }
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
        stage('Push to Docker Hub') {
            steps {
                // withCredentials keeps your password hidden in logs
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    bat """
                        docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                        docker tag nodejs-app %DOCKER_USER%/nodejs-devops-project:latest
                        docker push %DOCKER_USER%/nodejs-devops-project:latest
                    """
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