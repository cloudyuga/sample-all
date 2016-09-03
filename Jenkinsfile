node('dockerhost') {
  def appName = 'gceme'
  def imageTag = "cloudyuga/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"

  checkout scm

  stage 'Build image'
  sh("docker build -t ${imageTag} .")

  stage 'Run Go tests'
  sh("docker run ${imageTag} go test")

  stage 'Push image to registry'
  sh("docker push ${imageTag}")

  stage "Deploy Application"
  switch (env.BRANCH_NAME) {
    // Roll out to staging
    case "staging":
        sh("docker run -d --name=staging_gcme imageTag")
        break

    // Roll out to production
    case "master":
        sh("docker run -d --name=production_gcme -p 8080:80 imageTag")
        break

    // Roll out a dev environment
    default:
        // Create namespace if it doesn't exist
        sh("docker ps")
  }
}
