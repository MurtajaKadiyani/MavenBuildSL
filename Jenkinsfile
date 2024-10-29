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
		     bat "mvn clean install -Dmaven.test.skip=true"
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
		  steps
		  {
			script {
                    def tomcatUrl = 'http://52.172.211.198:8080'
                    def warFile = "target/*.war"
                    def contextPath = 'app'

                    sh """
                    curl -T ${warFile} ${tomcatUrl}/manager/text/deploy?path=/${contextPath}&update=true --user admin:admin
                    """
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
