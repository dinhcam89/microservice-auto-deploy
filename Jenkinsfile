pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dinhcam89-dockerhub')
        dockerImageName = "dinhcam89/react-app" // Adjusted variable name to follow convention
    }
    agent any
    stages {
        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build dockerImageName
                }
            }
        }
        stage('Login') {
            steps { 
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        // Use Docker Hub credentials to login
                        docker.login("${DOCKERHUB_CREDENTIALS_USR}", "${DOCKERHUB_CREDENTIALS_PSW}")
                    }
                }
            }
        }
        stage('Docker Tag') {
            steps {
                sh "docker tag react-app dinhcam89/react-app"
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploying React.js container to Kubernetes') {
            steps {
                script {
                    // You need to define `kubernetesDeploy` method or plugin properly
                    kubernetesDeploy(configs: "deployment.yaml", 
                                     "service.yaml")
                }
            }
        }
    }
}
