// Scripted

//Declarative pipeline
pipeline {
	agent any
	//agent{ docker{ image 'maven:3.6.3'}}
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps{
				sh 'mvn --version'
				//sh 'docker version'
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile'){
			steps{
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps{
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package'){
			steps{
				sh "mvn package -DskipTests"    // this will create a jar file and this jar file will be used to create docker image and push to Dockerhub
			}
		}
		stage('Build Docker Image'){
			steps{
				//docker build -t parivarababuk/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("parivarababuk/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('', 'dockerhub')  // picks the credentials for dockerhub from Cerdentials manager configureed in Jenkins dashboard
					{
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
	}
	post{
		success{
			echo 'I run when Build is success'
		}
		failure{
			echo 'I run when Build is failed'
		}
	}
	
}
