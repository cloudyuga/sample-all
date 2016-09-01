node {
  def appName = 'gceme'
  def feSvcName = "${appName}-frontend"
#  def imageTag = "gcr.io/${project}/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"
  def imageTag = "cloudyuga/sample-app"

  checkout scm

  stage 'Build image'
  sh("docker build -t ${imageTag} .")

  stage 'Run Go tests'
  sh("docker run ${imageTag} go test")

#  stage 'Push image to registry'
#  sh("gcloud docker push ${imageTag}")

}
