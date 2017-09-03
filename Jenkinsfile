
pipeline {
  agent {
    kubernetes {
      label 'golang-build'
      containerTemplate {
        name 'build'
        image 'golang:1.9.0-alpine3.6'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run Build') {
      steps {
        container('build') {
          sh 'CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .'
          sh 'docker build -t andrleite/godemo:v1.0 .'
        }
      }
    }
  }
}