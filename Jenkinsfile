pipeline {
agent any
tools {nodejs "nodenv"}
stages {
 stage("Code Checkout from GitHub") {
  steps {
   git branch: 'master',
    credentialsId: 'gitlab_access_token',
    url: 'http://your-ip-here:10080/root/test-project.git'
  }
 }
   stage('Code Quality Check via SonarQube') {
   steps {
       script {
       def scannerHome = tool 'sonarqube';
           withSonarQubeEnv("sonarqube-container") {
            nodejs(nodeJSInstallationName: 'nodenv'){
           sh "npm install"
             sh "npm run sonar"
           }
               }
           }
       }
   }
   
}
}
