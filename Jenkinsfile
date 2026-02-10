pipeline {
  agent any
  stages {
    stage('Install Dependencies') {
      steps {
        sh 'cd app && npm install'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'cd app && docker build -t nodejs-app .'
      }
    }
    stage('Run Container') {
      steps {
        sh '''
          docker rm -f nodejs-app || true
          docker run -d -p 3000:3000 --name nodejs-app nodejs-app
        '''
      }
    }
  }
}
