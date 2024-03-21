pipeline{

	agent any

	environment {
		DOCKERHB_CREDENTIALS = credentials('dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t react-app:latest .'
			}
		}

		stage('Check Docker') {
			steps {
				sh 'docker info'
			}
		}
		//comment

		stage('Login') {

			steps {	
				sh 'echo $DOCKERHB_CREDENTIALS_PSW | echo $DOCKERHB_CREDENTIALS_USR | docker login -u $DOCKERHB_CREDENTIALS_USR -p $DOCKERHB_CREDENTIALS_PSW'	
				}
		}
		
		
		stage('View Images') {

			steps {
				sh 'docker images'
			}
		}
		
		stage('Docker Tag') {

			steps {
				sh 'docker tag react-app dinhcam89/react-app'
			}
		}

		stage('Push') {

    		// some block
			steps{		
				sh 'docker push dinhcam89/react-app'					
			}
		
		}
        stage('Deploy with Minikube') {
            steps {
                sh 'minikube start' // Start Minikube
                sh 'kubectl apply -f deployment.yaml' // Create deployment
                sh 'minikube service react' // Open service in default browser
            }
        }

	
	}

	post {
		always {
			sh 'docker logout'
		}

		
	}

}