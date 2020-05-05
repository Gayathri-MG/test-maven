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
		
  }
}
