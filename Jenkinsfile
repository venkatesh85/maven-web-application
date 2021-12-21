node
{
def mavenHome = tool name: "maven3.8.4"
//echo "GitHub BranhName ${env.BRANCH_NAME}"
  //echo "Jenkins Job Number is: -->  ${env.BUILD_NUMBER}"
  echo "Jenkins Node Name is: --> ${env.NODE_NAME}"
  
  echo "Jenkins Home is: --> ${env.JENKINS_HOME}"
  echo "Jenkins URL is: -->  ${env.JENKINS_URL}"
  echo "JOB Name is: -->  ${env.JOB_NAME}"
  
  properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3')), pipelineTriggers([pollSCM('* * * * *')])])
 
stage('CheckOutCode')
{
git branch: 'development ', credentialsId: 'f6d6d507-448d-40bb-bbc6-6698dc726549', url: 'https://github.com/venkatesh85/maven-web-application.git'
}

stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
  
stage('ExcuteSonarQube Report')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('UploadArtifactInto')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppIntoTomcatServer')
{
sshagent(['216462b7-6240-4a81-8887-e73a0d35803c']){
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.108.234.249:/opt/apache-tomcat-9.0.54/webapps/"
}
}
stage ('SendEmailNotification')
{
emailext body: '''Buid Over - ScriptedWay.

Redards,
Venkatesh
9916412675''', subject: 'Buid Over - ScriptedWay', to: 'ravitheja.r1993@gmail.com'
}
}
