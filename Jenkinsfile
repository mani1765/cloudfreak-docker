pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JDK21'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('mani1765/cloudfreak-docker', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'mydocker') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
