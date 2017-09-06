#!/usr/bin/env groovy
podTemplate(label: 'docker', serviceAccount: 'jenkins', containers: [
  containerTemplate(name: 'docker', image: 'andrleite/k8s-builder', ttyEnabled: true, command: 'cat')],
  volumes: [
    hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock'),
    secretVolume(secretName: 'nexus-registry', mountPath: '/tmp/nexus-config')
  ]) {

  node('docker') {
    stage('Build') {
      git 'https://github.com/andrleite/k8s-godemo.git'
      container('docker') {
        sh "mkdir /home/jenkins/.docker && cp /tmp/nexus-config/.dockercfg /home/jenkins/.docker/config.json"
        sh "cat /home/jenkins/.docker/config.json"
        sh "docker build -t containers.lab.cloud104.io/godemo:$VERSION ."
        sh "docker push containers.lab.cloud104.io/godemo:$VERSION"
      }
    }
  }
  node('docker') {
    stage('Deploy') {
      git 'https://github.com/andrleite/k8s-godemo.git'
      container('docker') {
        sh "kops export kubecfg --name=k8s-service.cloud104.io --state=\"s3://kops-k8s-service-state\""
        sh 'kubectl set image deployment/godemo godemo=containers.lab.cloud104.io/godemo:\"${VERSION}\"'
        sh 'kubectl apply -f kubernetes/kube/'
      }
    }
  }
}