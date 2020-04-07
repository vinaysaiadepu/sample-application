def getDockerTag() {
 def tag = sh script: 'git rev-parse HEAD', returnStdout: true 
 return tag
}
pipeline{

	agent any
      environment {
          Docker_tag = getDockerTag()
      }
        
        stages{

              stage('build'){
		      steps {
			      script{
                sh 'docker build . -t vinaysai/devops-training:$Docker_tag'
                withCredentials([string(credentialsId: 'docker_password', variable: 'docker_password')]) {
    
                sh '''docker login -u vinaysai -p $docker_password
                docker push vinaysai/devops-training:$Docker_tag
		'''
                }
                
			      }
		      }
              }
		
            }	       	     	         
}



