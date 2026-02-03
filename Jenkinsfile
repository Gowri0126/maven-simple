pipeline {
	agent any
	
	environment {
		DOCKERHUB_CRED=credentials('dockerhub')
		IMAGE_NAME="maven-simple:1.0"
	}
	
	stages {
		stage('checkout') {
			steps {
				git url:'https://github.com/Gowri0126/maven-simple.git', branch:'main'
			}
		}

		stage('Build Maven Project') {
			steps {
				sh "mvn clean package -DskipTests"
			}
		}
		
		stage('Build Docker Image') {
            		steps {
                		script {
                    			dockerImage = docker.build("maven-simple:1.0")
                		}
            		}
        	}

		stage('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('https://index.docker.io/v1/','dockerhub'){
						dockerImage.push()
					}
				}
			}
		}	
	}
	
	post {
		success {
			echo "Pipeline Successful"
		}
		failure {
			echo "Pipeline Failure"
		}
		always {
			echo "Cleaning workspace"
			deleteDir()
		}
	}
	

}
