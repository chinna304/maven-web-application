node
{
 def mavenHome = tool name:"maven3.6.3"
 
 stage('checkout code')
 {
 git branch: 'development', credentialsId: '8b048c9d-c9b9-4236-aff9-245c0c6b37f6', url: 'https://github.com/chinna304/maven-web-application.git'
 }
 stage('Build')
 {
 sh "${mavenHome}/bin/mvn clean package"
 }
 stage ('Execute Sonar Qube Report')
 {
 sh "${mavenHome}/bin/mvn sonar:sonar"
 }
 stage ('Upload Arftifactory into Nexus')
 {
 sh "${mavenHome}/bin/mvn deploy"
 }
 stage ('Deploy application in tomcat server')
 {
 sshagent(['6eab8479-ebc7-4370-b634-bb9a878422c2']) 
 {
 sh "scp  -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@52.202.52.239:/opt/apache-tomcat-9.0.38/webapps/"
 }
 }
 stage ('Email Notification')
 {
 mail bcc: '', body: 'Build is over ', cc: '', from: '', replyTo: '', subject: 'Build is over', to: 'chinna996611@gmail.com,chinnasetty304@gmail.com'
 }
 
}
