node{
    
def mavenHome = tool name: 'maven3.8.5'
echo "The job name is :  ${env.JOB_NAME} "
echo "The build no.: ${env.BUILD_NUMBER}"
echo "The node name is : ${env.NODE_NAME}"

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

}//node closing 
