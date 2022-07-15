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
		stage ('check-git-secrets') {
		steps {
			sh'rm trufflhog || true'
			sh'docker pull gesellix/trufflehog'
			sh'docker run -t gesellix/trufflehog --json .git > trufflehog'	
			sh 'cat trufflehog'
 		}

		
		
		stage ('build') {
			steps {
			 	sh 'mvn clean package'
                		
			      }
			        }
		stage ('deploy-to-tomcat') {
		  steps {
			sh'sshpass -p "ajay123" scp -o StrictHostkeyChecking=no target/*.war root@192.168.80.101:/opt/tomcat/apache-tomcat-9.0.64/webapps/webapp.war'
			
			}

		} 
             }
	}
