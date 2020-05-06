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
	  stage('s3Upload') {
		  steps{
			  s3Upload acl: 'Private', bucket: '25march2020', cacheControl: '', excludePathPattern: '', file: 'java-fullstack-1.0-SNAPSHOT.jar', includePathPattern: '', metadatas: [''], redirectLocation: '', sseAlgorithm: '', text: '', workingDir: 'dist'
		  }
  }
  }
}
