pipeline {
	//agent any
	agent { 
		any { 
			image 'node:13.8'
			} 
		}
	stages {
		stage('Build') {
			steps{
				echo "Build"
				sh 'node --version'
			}			
		}
		stage('Test') {
			steps{
				echo "test"
			}
		}
		stage('Integration') {
			steps{
				echo "integration"
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
