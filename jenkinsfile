node{
    
echo "Jenkins Home directory is:${env.JENKINS_HOME}"
echo "Job name is:${env.JOB_NAME}"
echo "Build number is:${env.BUILD_NUMBER}" 

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false], [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

def mavenHome=tool name: 'maven3.9.3'

stage('CheckOutCode'){
git branch: 'development', credentialsId: 'd7d2012d-8d73-487b-a8bf-4f9cf748ac26', url: 'https://github.com/VenkatBalisetty/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('UploadArtifactsIntoNexus'){
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcatServer'){
sshagent(['29fc441d-083b-4171-a091-8a13fce6ddd6']) {
sh "scp -o StrictHostkeyChecking=no target/maven-web-application.war ec2-user@172.31.42.190:/opt/apache-tomcat-9.0.76/webapps"
}  
}
*/
}
