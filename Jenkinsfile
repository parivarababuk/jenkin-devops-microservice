// Scripted

//Declarative pipeline
pipeline {
	agent any
	stages{
		stage('Build'){
			steps{
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
			echo 'I rum when Build is success'
		}
		failure{
			echo 'I rum when Build is failed'
		}
	}
	
}
