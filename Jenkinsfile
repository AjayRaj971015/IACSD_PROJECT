pipeline{
	agent any
	tools{
		maven 'Maven'
	     }
	stages{
		stage (Initialize) {
		steps {
			sh '''
				echo "PATH = ${PATH}"
				echo "M2_HOME = ${M2_HOME}"
			    '''
		      }
 			            }
		stage ('build') {
			steps {
			 	sh 'mvn clean package'
                		
			      }
			        }
		stage ('deploy-to-tomcat') {
		  steps {
		sshagent(['tomcat']) {
			sh 'scp -o StrictHostkeyChecking=no /var/lib/jenkins/workspace/testing_pro/target/*.wars root@192.168.80.101:/opt/tomcat/apache-tomcat-9.0.64/webapp.war'
			}		

			}

		} 
             }
	}
