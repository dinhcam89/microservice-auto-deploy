pipeline {
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dinhcam89-dockerhub')
    dockerimagename = "dinhcam89/react-app"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Login') {

			steps {	
				sh 'echo $DOCKERHB_CREDENTIALS_PSW | echo $DOCKERHB_CREDENTIALS_USR | docker login -u $DOCKERHB_CREDENTIALS_USR -p $DOCKERHB_CREDENTIALS_PSW'	
				}
		}
    stage('Docker Tag') {

			steps {
				sh 'docker tag react-app" dinhcam89/react-app"'
			}
		}

		stage('Push') {

    		// some block
			steps{		
				sh 'docker push dinhcam89/react-app"'					
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