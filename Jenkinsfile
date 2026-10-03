pipeline{
    agent any
    tools{
        maven "maven-3.9.16"
    }
    stages{
        stage('git checkout'){
            steps{
                  git branch: 'QA', url: 'https://github.com/critical-river/maven-webapplication-project-kkfunda.git'
            }
        }
        stage('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('SQ Report'){
            steps{
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar'
            }
        }
        stage('deploy'){
            steps{
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar deploy'
            }
        }
        stage('Tomcat deployment'){
            steps{
                 sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/Declarativeway-pipeline/target/maven-web-application.war \
"http://43.204.221.54:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
            }
        }
    }
} 

