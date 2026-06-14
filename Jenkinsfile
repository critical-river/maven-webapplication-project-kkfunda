node
{

   def mavenHome= tool name: "maven_3.9.6"
   stage('git checkout')
   {
      git branch: 'master', url: 'https://github.com/critical-river/maven-webapplication-project-kkfunda.git'
   }
   stage('COMPILE')
   {
    sh  "${mavenHome}/bin/mvn compile" 
   }
   stage('Build'){
       sh "${mavenHome}/bin/mvn clean package"
   }
  stage('Sonar REPORT'){
       sh "${mavenHome}/bin/mvn clean sonar:sonar"
  }
       stage('deploy to nexus'){
           sh "${mavenHome}/bin/mvn deploy"
       }
       stage('Deploy to Tomcat') 
    {
      
      sh """
curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/scripted-way-pipleline/target/maven-web-application.war \
"http://13.218.233.154:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }
	
   }
