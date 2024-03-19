pipeline {
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dinhcam89-dockerhub')
    dockerimagename = "dinhcam89/react-app"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/dinhcam89/microservice-auto-deploy'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    
    stage('Pushing Image') {
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", 
                                         "service.yaml")
        }
      }
    }
  }
}