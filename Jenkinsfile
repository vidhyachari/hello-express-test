node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"

    //sh "git rev-parse --short HEAD > commit-id"

    tag = "latest"
    appName = "hello-express"
    //registryHost = "127.0.0.1:30400/"
    imageName = "${appName}:${tag}"
    env.BUILDIMG=imageName

    stage "Build"

        sh "docker build -t ${imageName} ."

    stage "Push"

        sh "docker push ${imageName}"

    stage "Deploy"

        sh "sed 's#hello-express:latest#'$BUILDIMG'#' kubernetes-templates-yaml/deployment.yaml | kubectl apply -f -"
        sh "kubectl rollout status deployment/hello-express"
}
