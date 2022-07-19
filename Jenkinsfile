pipeline{
	agent any
	tools{
		maven 'Maven'
	     }
	stages{
		stage ('Initialize') {
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
			sh'docker run -t gesellix/trufflehog --json https://github.com/AjayRaj971015/IACSD_PROJECT.git > trufflehog'	
			sh 'cat trufflehog'
 		      }

				             }
		
		stage ('Dependency Check') {
		steps {
			sh 'rm owasp* || true'
			sh 'wget "https://raw.githubusercontent.com/AjayRaj971015/IACSD_PROJECT/master/DC.sh"'
			sh 'chmod +x DC.sh'
			sh './DC.sh || true '
	
			}
 			}
		stage('SAST') {
		steps {
		withSonarQubeEnv('sonar') {
			//sh 'mvn sonar:sonar'
			sh 'mvn sonar:sonar -Dsonar.projectKey=group1 -Dsonar.host.url=http://192.168.80.100:9000 -Dsonar.login=sqa_76829e1cdc1af5936e79ac3d0cb50d5f4f13c5c8 || true'
			sh 'cat target/sonar/report-task.txt'
		}

	}
	}

		stage ('build') {
			steps {
			 	sh 'mvn clean package'
                		
			      }
			        }
		stage ('deploy-to-tomcat') {
		  steps {
		  //sshagent(['192.168.80.101'])
			sh'cd $WORKSPACE'
			sh'sshpass -p "ajay123" scp -o StrictHostkeyChecking=no target/WebApp.war root@192.168.80.101:/opt/tomcat/apache-tomcat-9.0.64/webapps/webapp.war'
			  
			}

		} 
             }
	}
