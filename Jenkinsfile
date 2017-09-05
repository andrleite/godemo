#!/usr/bin/env groovy
podTemplate(label: 'docker', serviceAccount: 'jenkins', containers: [
  containerTemplate(name: 'docker', image: 'andrleite/demobuild', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
) {

  node('docker') {
    stage('Build') {
      git 'https://github.com/andrleite/k8s-godemo.git'
      container('docker') {
        sh "docker build -t containars.lab.cloud104.io/godemo:$VERSION ."
        sh "docker push containars.lab.cloud104.io/godemo:$VERSION"
      }
    }
  }
}