pipeline
{
	agent any
	
	stages
	{
		stage('Checkout Code')
		{
		  steps
		  {
			 checkout scm
		  }
		}
	
	    stage('Build')
	    {
		  steps
		  {
		     sh "mvn clean install -Dmaven.test.skip=true"
		  }
	    }
	
	    stage('Archive Artifact')
		{
		  steps
		  {
			archiveArtifacts artifacts:"target/*.war"
		  }
		}
	
		stage('deployment')
		{
		  stage('Deploy to tomcat') 
		  {
            steps 
			{
               deploy adapters: [tomcat10(credentialsId: 'TomcatCreds', path: '', url: 'http://52.172.211.198:8080')], contextPath: null, war: 'target/*.war'
            }
          }
			
		}
		
		stage('Notification')
		{
			steps
			{
			  emailext(
				subject: "Job Completed",
				body: "Jenkins pipeline job for maven build job completed",
				to: "murtaja.mainframe@gmail.com")
			}
		}
	}
   }

