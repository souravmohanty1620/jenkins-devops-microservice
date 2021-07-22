pipeline {
	agent any
	//agent { 
		//any { 
			//image 'node:13.8'
			//} 
		//}
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'mymaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps{
				echo "Build"
				sh 'mvn --version'
				sh 'docker version'
				echo "$PATH - $env.PATH"
				echo "$BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "$BUILD_ID - $env.BUILD_ID"
				echo "$JOB_NAME - $env.JOB_NAME"
				echo "$BUILD_TAG - $env.BUILD_TAG"
				echo "$BUILD_URL - $env.BUILD_URL"

			}			
		}
		stage('Compile') {
			steps{
				sh "mvn clean compile"
			}
		}

		stage('test') {
			steps{
				sh "mvn test"
			}
		}

		stage('Integration') {
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package') {
			steps{
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image') {
			steps{
				//docker build -t sourav2016/hello-world-python:$env.BUILD_TAG
				script{
					dockerImage = docker.build(sourav2016/hello-world-python:${env.BUILD_TAG})
				}
			}
		}
		stage('Push Docker Image') {
			steps{
				//sh "mvn failsafe:integration-test failsafe:verify"
				script {
					docker.withRegistry('','dockerhub') {
					dockerImage.push();
					dockerImage.push('latest');
					}
				}
			}
		}

	}

	post {
		always {
			echo 'i am awesome'
		}
		success {
			echo 'i run when you are success'
		}
		failure {
			echo 'i run when u fail'
		}
	}
}
