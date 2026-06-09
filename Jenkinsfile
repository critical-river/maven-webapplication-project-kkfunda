
node {
    def mavenHome= tool name:'maven-3.9.16'
    stage('git checkout'){
        git branch: 'master', url: 'https://github.com/critical-river/maven-webapplication-project-kkfunda.git'
    }
    stage('maven compile'){
        sh "${mavenHome}/bin/mvn compile"
    }
    stage('maven build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('sonar Qube report'){
        sh "${mavenHome}/bin/mvn package sonar:sonar"
    }
    stage('nexus'){
        sh "${mavenHome}/bin/mvn deploy"
    }
  stage('Deploy to Tomcat') {
    echo "Deploying WAR file using curl..."

    sh """
        curl -u kk:password \
        --upload-file /var/lib/jenkins/workspace/scripted-way-pipleline/target/maven-web-application.war \
        "http://98.83.39.187:8080/manager/text/deploy?path=/maven-web-application&update=true"
    """
}

}
