node
{

    def mavenHome = tool name: "maven3.8.6"
    //properties([[$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

stage('CheckoutCode')
    {
    git branch: 'development', credentialsId: '684beece-d175-4f5e-b53b-aa1edb7a41f5', url: 'https://github.com/nss-ecom-projectapps/maven-web-application.git'
    }

stage('Build')
    {
    sh "${mavenHome}/bin/mvn clean package"
    }

/*
stage('ExecuteSonarQubeReport')
    {
    sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
stage('UploadArtifactsintoNexus')
{
sh "${mavenHome}/bin/mvn deploy"
}

stage('DeployAppintoTomcatServer')
{
sshagent(['ed4ccb5a-c8d7-4812-aed2-0f5a336abc65']) {
sh "scp -o StrictHostKeyChecking=no target.maven-web-application.war <username>@ipaddress-of-linux-server:/opt/apache-tomcat-9.0.65/webapps/"
}
}
*/

stage('SendEmailNotification')
{
emailext body: '''Build Success.

Regards,
ForeFendTech.''', subject: 'Build Success', to: 'venkatactaladi@gmail.com'
}

}
