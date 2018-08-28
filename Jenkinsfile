node{
   stage("ACM checkout"){
       git 'https://github.com/joshimahesh/sampleapp'
    }
    stage("Compile-Package"){
       def mvnHome = tool name: 'maven-3', type: 'maven'
     sh "${mvnHome}/bin/mvn package"
    }
    stage("Slack Notification")
    {
        slackSend baseUrl: 'https://hooks.slack.com/services/', 
        channel: '#jenkins-pipeline-demo',
        color: 'good', 
        message: 'Welcome to Jenkins!! Slack notification.',
        teamDomain: 'bitwise-demoworkspace', 
        tokenCredentialId: 'slack-demo'
   }
 
}
