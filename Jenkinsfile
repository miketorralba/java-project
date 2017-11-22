properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/miketorralba/java-project.git'
		sh 'ant -f test.xml -v'   
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Results') {    
		junit 'reports/result.xml'   
	}
	stage('Deploy') {    
		sh 'cp rectangle-${BUILD_NUMBER}.jar jenkins-s3bucket-1gkpskz7vsi2g.s3.amazonaws.com'   
	}
	stage('Report') { 
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '31f55ea0-bbbf-4235-b46d-b372ca3af836', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
      sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
      }   
		   
	}
	
}
