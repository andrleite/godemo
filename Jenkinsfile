#!/usr/bin/env groovy
podTemplate(label: 'docker', serviceAccount: 'jenkins', containers: [
  containerTemplate(name: 'docker', image: 'andrleite/demobuild', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
) {

  node('docker') {
    stage('Build') {
      container('docker') {
        sh "docker build -t andrleite/godemo:$VERSION ."
      }
    }
  }
}