pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('sameep-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t sameeps/dp-alpine:3.13.5 .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push sameeps/dp-alpine:3.13.5'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}