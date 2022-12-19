node{
    try {   

def mavenHome = tool name: 'maven3.8.5'
echo "The job name is :  ${env.JOB_NAME} "
echo "The build no.: ${env.BUILD_NUMBER}"
echo "The node name is : ${env.NODE_NAME}"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
//CehckoutCode stage
stage ('CheckoutCode'){
    
git branch: 'development', credentialsId: '4a56eaed-eb93-47d6-9f27-2acb933d748a', url: 'https://github.com/laxmishiwarkar/maven-web-application.git'
}
//Build
stage('Build'){
sh "${mavenHome}/bin/mvn clean package "
}
/*
// Execute SonarQube Report
stage('ExecuteSonarQubReprt'){
sh "${mavenHome}/bin/mvn sonar:sonar"                                        
}

// Upload ArtifactsInto Nexus 
stage('UploadArtifactsIntoNexus'){
sh "${mavenHome}/bin/mvn deploy"     

}
//Deploy App into Tomcat Server 
stage ('DeployApp'){

sshagent(['67759de7-550b-4350-8f64-22a3b6692e64']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.25.9:/opt/apache-tomcat-9.0.68/webapps/"
}
}
*/

    }// try closing 
 catch (e) {
currentBuild.result= "FAILURE"
}
 finally {

// Success or failure, always send notifications
sendSlackNotifications(currentBuild.result)

}


}//node closing 
//Function for slack notification 
def sendSlackNotifications(StringbuildStatus = 'STARTED') {
  // build status of null means successful
buildStatus =  buildStatus ?: 'SUCCESS'
// Default values
def colorName = 'RED'
def colorCode = '#FF0000'
def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
def summary = "${subject} (${env.BUILD_URL})"
// Override default values based on build status
if (buildStatus == 'STARTED') {
    color = 'YELLOW'
colorCode = '#FFFF00'
} else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'colorCode = '#00FF00'
}  else {
    color = 'RED'colorCode = '#FF0000'}
// Send notifications
slackSend (color: colorCode, message: summary)
}


