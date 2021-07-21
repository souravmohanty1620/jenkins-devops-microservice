pipeline {
	//agent any
	agent { 
		any { 
			image 'maven:3.6.3'
			} 
		}
	stages {
		stage('Build') {
			steps{
				echo "Build"
				sh 'mvn --version'
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
