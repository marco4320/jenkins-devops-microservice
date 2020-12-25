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
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				echo "Checkout"
				sh 'mvn --version'
				sh 'docker version'
				echo "PATH: $PATH"
				echo "BUILD_NUMBER: $env.BUILD_NUMBER"
				echo "BUILD_ID: $env.BUILD_ID"
				echo "JOB_NAME: $env.JOB_NAME"
				echo "BUILD_TAG: $env.BUILD_TAG"
				echo "BUILD_URL: $env.BUILD_ID"
			}
		}
		stage('Compile') {
			steps {
				echo "Compile"
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				echo "Test"
				//sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Package') {
			steps {
				echo "Build Jar"
				sh 'mvn package -DskipTests'
			}
		}
		stage('Build Docker Image') {
			steps {
				echo "Build Docker Image"
				//"docker build -t mk2020id/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("mk2020id/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				echo "Push Docker Image"
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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
