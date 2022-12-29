node{
    
    def Home = tool name: "maven3.8.6"
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
    echo "Build Number is: ${env.BUILD_NUMBER}"
    echo "Node Name is: ${env.NODE_NAME}"
    echo "Job Name is: ${env.JOB_NAME}"
    try {
    stage('Checkoutcode')
    {
        git credentialsId: 'f39798bd-8dbb-4b53-9928-bcf2c8c9844f', url: 'https://github.com/sonu-devops-40/maven-web-application.git'
    }
    stage('Build')
    {
        sh "${Home}/bin/mvn clean package"
    }
    /*
    stage('Execute sonarqube report')
    {
        sh"${Home}/bin/mvn sonar:sonar"
    }
    stage('Upload Into Artifactory Repository')
    {
        sh"${Home}/bin/mvn deploy"
    }
    stage('Deploy the Apllication to tomcat server')
    {
        sshagent(['b9da946c-de8d-4e65-8232-fff17fa16727'])
        {
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.3.90:/opt/apache-tomcat-9.0.70/webapps"
        }
    }
    */
    }catch (e) {
    // If there was an exception thrown, the build failed
    currentBuild.result = "FAILED"
    throw e
  } finally {
    // Success or failure, always send notifications
    notifyBuild(currentBuild.result)
  }
}
