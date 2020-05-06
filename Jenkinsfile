pipeline {

 agent any
 
 
  options {
     skipDefaultCheckout()
  }
	
  stages {
  
	stage('Checkout from GIT') {
        steps {
           	script {
					git branch: "${BRANCH}", credentialsId: '	7f4298e8-bbd6-4280-b629-4c1206ce3147', url: 'https://github.com/Gayathri-MG/test-maven.git'
				    gitInfo = checkout scm
                    echo "Current Branch : $gitInfo.GIT_COMMIT"
					println gitInfo
            }
        }
    }
	  stage('Build') {
		steps {
			script {
				sh '''
				mvn --version
				cd ${WORKSPACE}
				mvn -Dmaven.test.skip -Pcomplete-build clean install
				'''
			}
		}
	}
	  stage('Upload') {
		  steps{
        	dir('/var/lib/jenkins/workspace/Maven-build/target/'){
            pwd(); //Log current directory
            withAWS(region:'us-west-2',credentialsID:'123456') {
                 def identity=awsIdentity();//Log AWS credentials
                // Upload files from working directory 'dist' in your project workspace
                s3Upload(bucket:"25march2020", workingDir:'target', includePathPattern:'**/*');
            }
        }
		  }}
  }
}
