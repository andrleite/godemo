
pipeline {
  agent {
    kubernetes {
      label 'mypod'
      containerTemplate {
        name 'test'
        image 'scratch'
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