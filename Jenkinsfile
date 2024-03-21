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

	
	}

	post {
		always {
			sh 'docker logout'
		}

		
	}

}