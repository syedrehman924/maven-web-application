node
{
    def mavenHome = tool name:"maven3.8.3" 
     
	stage('Checkout SCM')
	{
		git branch: 'development', credentialsId: '232d40fc-77db-4e01-bac3-131f8ac9e01c', url: 'https://github.com/ecom-website/maven-web-application.git'
	}
	
	stage('Build')
	{
		sh "${mavenHome}/bin/mvn clean package"
	}
	
		stage('Sonar')
	{
		sh "${mavenHome}/bin/mvn clean sonar:sonar"
	}
	
		stage('Nexus')
	{
		sh "${mavenHome}/bin/mvn clean deploy"
	}	

	stage('Deploy to Tomcat')
	{
		sshagent(['30d90ff4-a3ea-4324-ba32-86fe95cde5f9']) {
		sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.110.55:/opt/apache-tomcat-9.0.58/webapps/"
         }
    }	
	
}
