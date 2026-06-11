pipeline {
    agent any
    tools{
        maven 'maven-3.9.16'
    }

    stages {
        stage('git checkout') {
            steps {
               git branch: 'master', url: 'https://github.com/critical-river/maven-webapplication-project-kkfunda.git'
            }
        }
        stage('maven compile'){
            steps{
               sh 'mvn compile' 
            }
        }
         stage('maven Build'){
            steps{
               sh 'mvn clean package' 
            }
        }
         stage('sonar Qube'){
            steps{
               sh 'mvn sonar:sonar' 
            }
        }
         stage('nexus'){
            steps{
               sh 'mvn deploy' 
            }
        }
        stage('deploy to tomcat'){
            steps{
                  sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/Declarative_way_pipeline/target/maven-web-application.war \
"http://100.48.50.227:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
            }
        }
    }
}
