pipeline {
    // add your slave label name
    agent { label 'jenkins-maven-slave'}
    tools{
        maven 'maven'
    }
    stages {
        stage ('Checkout_SCM') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('Maven_Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('Deploy_Tomcat') {

            steps {
	      sshagent(['tomcat_server']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@3.108.65.191:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
