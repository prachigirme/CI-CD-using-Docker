pipeline {
    agent any
	
	  tools
    {
       maven "maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp prachi11/samplewebapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
          sh  'docker push prachi11/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8005:8080 prachi11/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H 18.208.245.128 run -d -p 8005:8080 prachi11/samplewebapp"
 
            }
        }
    }
	}
    
