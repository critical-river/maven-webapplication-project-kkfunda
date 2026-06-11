node{
    def mavenHome= tool name:"maven-3.9.16"
    stage('git checkout'){
        git branch: 'master', url: 'https://github.com/critical-river/maven-webapplication-project-kkfunda.git'
    }
    stage('mvn compile'){
        sh "${mavenHome}/bin/mvn compile"
    }
    stage('mvn build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('maven Sonar Qube report'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('nexus stage'){
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('Deploy to Tomcat') 
    {
      sh '''
curl -u kk:password \
  --upload-file "/var/lib/jenkins/workspace/scripted way pipleline/target/maven-web-application.war" \
  "http://100.48.50.227:8080/manager/text/deploy?path=/maven-web-application&update=true"
'''
    }
}//end of the node
