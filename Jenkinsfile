
pipeline {
  agent none
  stages {
    stage('Build') {
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
      steps {
        container('build') {
          sh 'CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .'
        }
      }
    }
    stage('Deploy') {
      agent {
        kubernetes {
          label 'alpine-deploy'
          containerTemplate {
            name 'deploy'
            image 'byrnedo/alpine-curl'
            ttyEnabled true
            command 'cat'
          }
        }
      }
      steps {
        container('deploy') {
          sh 'TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token) && curl https://api.k8s-service.cloud104.io/api/v1/namespaces/jenkins/pods --header \"Authorization: Bearer \$TOKEN\" --insecure'
        }
      }
    }
  }
}