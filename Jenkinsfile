node {
  def appName = 'gceme'
  def feSvcName = "${appName}-frontend"
  def imageTag = "cloudyuga/sample-app"

  checkout scm

  stage 'Build image'
  sh("docker build -t ${imageTag} .")

  stage 'Run Go tests'
  sh("docker run ${imageTag} go test")


}
