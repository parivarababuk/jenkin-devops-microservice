// Scripted

//Declarative pipeline
pipeline {
	//agent any
	agent{
		docker{
			image 'maven:3.6.3'
		}
	}
	stages{
		stage('Build'){
			steps{
				sh 'mvn --version'
				echo "Build"
			}
		}
		stage('Test'){
			steps{
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
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
