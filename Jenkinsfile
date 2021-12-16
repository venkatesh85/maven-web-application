node
{
def mavenHome = tool name: "maven3.8.4"

stage('CheckOutCode')
{
git branch: 'development ', credentialsId: 'f6d6d507-448d-40bb-bbc6-6698dc726549', url: 'https://github.com/venkatesh85/maven-web-application.git'
}

stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
  /*
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
sshagent(['544b76c0-0348-4ea6-bedd-e28729d6e1b5']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.13.171:/opt/apache-tomcat-9.0.54/webapps/"
}
}
*/
stage ('SendEmailNotification')
{
emailext body: '''Buid Over - ScriptedWay.

Redards,
Venkatesh
9916412675''', subject: 'Buid Over - ScriptedWay', to: 'ravitheja.r1993@gmail.com'
}
}
