
  node 
{
   //     /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.16/bin

   def mavenHome=tool name: "maven-3.9.16"
  stage('git checkout')
  {
      git branch: 'master', url: 'https://github.com/kkdevopsb10/maven-webapplication-project-kkfunda.git'
  }
  stage('compile')
  {
   sh "${mavenHome}/bin/mvn compile"
  }
   stage('Build')
  {
   sh "${mavenHome}/bin/mvn clean package"
  }
  /* stage('SQ REPORT')
  {
   sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  stage('Deploy Artifact')
  {
   sh "${mavenHome}/bin/mvn deploy"
  }*/


    stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/MBPL-webapp/target/maven-web-application.war \
"http://16.112.192.134:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }

	
	
}  // node end  

