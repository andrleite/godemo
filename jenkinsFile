pipeline {
  agent {
    kubernetes {
      label 'test-pod'
      containerTemplate {
        name 'test-pod'
        image 'scratch'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Test') {
      steps {
        container('test-pod') {
          sh 'echo TEST'
        }
      }
    }
  }
}