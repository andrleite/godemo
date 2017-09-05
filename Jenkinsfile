podTemplate(label: 'docker', serviceAccount: 'jenkins', containers: [
  containerTemplate(name: 'docker', image: 'andrleite/demobuild', ttyEnabled: true, command: 'cat')
], volumes: [hostPahVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
) {

  node('docker') {
    stage('Build') {
      container('docker') {
        sh "docker build -t andrleite/godemo:$VERSION ."
      }
    }
  }
}