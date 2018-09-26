def mvnHome
pipeline{
	agent any
	stages{
		stage('Preperation'){
			steps{
				// Get the Maven tool.
				// ** NOTE: This 'M3' Maven tool must be configured
				// **       in the global configuration. 
				script{
					mvnHome = tool 'M3'
				}          
			}
		}
		stage('Build'){
			when{ 
				expression {isUnix()}
			}
			steps{
				echo "Building on Unix"
			    sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"

			}
		}

		stage('Master Branch stuff'){
			when{
				/* conditions everything needs to be true*/
				branch 'master'
			}
			steps{
				echo 'master branch'
			}

		}
		/*Stashing artifacts either copyArtifact pipe or use stash*/

		stage('Results') {
			steps{
				junit '**/target/surefire-reports/TEST-*.xml'
				archive 'target/*.jar'
			}
   		}	
	}
}