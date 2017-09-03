
pipeline {
  agent {
    kubernetes {
      label 'mypod'
      containerTemplate {
        name 'test'
        image 'golang:1.9.0-alpine3.6'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run Test') {
      steps {
        container('test') {
          sh 'echo TEST'
        }
      }
    }
  }
}