// scripted pipeline
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

// declarative pipeline
pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'} }
	stages {
		stage('Build') {
			steps {
				echo "Build"
				//sh 'mvn --version'
				echo "PATH: $PATH"
				echo "BUILD_NUMBER: $env.BUILD_NUMBER"
				echo "BUILD_ID: $env.BUILD_ID"
				echo "JOB_NAME: $env.JOB_NAME"
				echo "BUILD_TAG: $env.BUILD_TAG"
				echo "BUILD_URL: $env.BUILD_ID"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	}
	// declare what do do after stages completion
	post {
		always {
			echo "Stage processing done."
		}
		success {
			echo "This was a success."
		}
		failure {
			echo "This was a failure."
		}
		// changed {}  // when the status of a build changes

	}
}
