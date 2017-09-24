podTemplate(label: 'pod-jenkins-slave',
  containers: [containerTemplate(name: 'jenkins-slave', image: 'jenkinsci/jnlp-slave:latest', ttyEnabled: true, command: 'cat')]
  //volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "hello-express"
  node('docker') {
    stage('Build Docker image') {
      git 'https://github.com/vidhyachari/hello-express-test.git'
      container('jenkins-slave') {
        sh "docker build -t ${image} ."
      }
    }
  }
}


// node('default-jenkins-slave') {
//
//     checkout scm
//
//     env.DOCKER_API_VERSION="1.23"
//
//     sh "git rev-parse --short HEAD > commit-id"
//
//     tag = "latest"
//     appName = "hello-express"
//     //registryHost = "127.0.0.1:30400/"
//     imageName = "${appName}:${tag}"
//     env.BUILDIMG=imageName
//
//     stage "list images"
//
//         sh "docker images"
//
//     stage "Build"
//
//         sh "docker build -t ${imageName}"
//
//     stage "Push"
//
//         sh "docker push ${imageName}"
//
//     stage "Deploy"
//
//         sh "sed 's#hello-express:latest#'$BUILDIMG'#' kubernetes-templates-yaml/deployment.yaml | kubectl apply -f -"
//         sh "kubectl rollout status deployment/hello-express"
// }
