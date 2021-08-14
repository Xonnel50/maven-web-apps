//Jenkins pipeline script
//Groovy script 

node{
  def mavenHome = tool name: 'maven3.8.1'
  stage('CodeClone') {
    
    git credentialsId: 'Git', url: 'https://github.com/Xonnel50/maven-web-apps.git'
  }
  stage('mavenBuild') {
    sh "${mavenHome}/bin/mvn clean package"
  }

  stage('CodeQuality') {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  // execute the CodeQuality report with sonar
  }
  stage('emailQualityIssues') {
    emailext body: '''Thanks

Landmark Technologies''', recipientProviders: [developers()], subject: 'status of build', to: 'mylandmarktech@gmail.com'
  }

   stage('UploadNexus') {
    sh "${mavenHome}/bin/mvn deploy"
    //mvn deploy  are uploaded in to nexus
  }

  stage('DeployTomcat') {
   deploy adapters: [tomcat9(credentialsId: 'Tomcat2', path: '', url: 'http://3.80.37.191:8080/')], contextPath: null, war: 'target/*war'     
  }
  stage('emailDeployIssues') {
    emailext body: '''Thanks
emailext body: 'Please fix listed issues', recipientProviders: [developers()], subject: 'Issues', to: 'lennoxbailey@yahoo.com'
      
  }

}
