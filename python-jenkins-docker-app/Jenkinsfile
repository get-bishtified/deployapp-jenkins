pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t python-jenkins-app .'
      }
    }

    stage('Run Docker Container') {
      steps {
        sh '''
          docker rm -f python-jenkins-app || true
          docker run -d -p 5000:5000 --name python-jenkins-app python-jenkins-app
        '''
      }
    }
  }

  post {
    success {
      echo 'Docker-based Python app deployed successfully.'
    }
  }
}
