pipeline {
  agent {
    kubernetes {
      label 'build'
      serviceAccount 'jenkins'
      containerTemplate {
        name 'build'
        image 'andrleite/demobuild'
        ttyEnabled true
        command 'cat'
        privileged true
        // volumes{
        //   hostPathVolume {
        //     hostPath '/var/run/docker.sock' 
        //     mountPath '/var/run/docker.sock'
        //     }
          }
        }
      }
    }
  stages {
    stage('Build') {
      steps {
        container('build') {
          sh "docker build -t andrleite/godemo:$VERSION ."
        }
      }
    }
    stage('Deploy') {
      steps {
        container('deploy') {
          echo 'TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token) && kubectl --token \"${TOKEN}\" set image deployment/godemo godemo=andrleite/godemo:\"${VERSION}\"'
        }
      }
    }
  }
}