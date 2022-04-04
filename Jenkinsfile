node
{

  def call(String buildStatus = 'STARTED') {
  // build status of null means successful
  //This is the condition which we are checking weather buildStatus is SUCCESSFULL or not.
 //This line updated to show the Eclipse with GitHub demo...
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
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Calling the slackSend function to Send notifications...
  slackSend (color: colorCode, message: summary)
}
  
  def mavenHome = tool name: "maven3.8.5"
  
  stage('CheckoutCode')
  {
  git branch: 'development', credentialsId: '1a45899f-9350-4d96-9894-42c222d595e3', url: 'https://github.com/mss-ec-apps-novbatchanil/maven-web-application.git'
  }

  stage('Build')
  {
  sh "${mavenHome}/bin/mvn clean package"
  }
  /*
  stage('ExecuteSonarqubeReport')
  {
  sh "${mavenHome}/bin/mvn clean sonar:sonar"
  }
  
  stage('UploadArtifactintoNexus')
  {
  sh "${mavenHome}/bin/mvn clean deploy"
  }
  
  stage('DeployAppIntoTomcat')
  {
  sshagent(['5c9bd688-00af-4114-b318-ed985664fcae']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.127.17.200:/opt/apache-tomcat-9.0.59/webapps"
}
  }
  */
  notifyBuild(currentBuild.result)
}
