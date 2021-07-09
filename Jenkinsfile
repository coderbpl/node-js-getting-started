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
           sh "${tool("sonarqube")}/bin/sonar-scanner \
           -Dsonar.projectKey=test-node-js \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://your-ip-here:9000 \
           -Dsonar.login=your-generated-token-from-sonarqube-container"
               }
           }
       }
   }
   stage("Install Project Dependencies") {
   steps {
       nodejs(nodeJSInstallationName: 'nodenv'){
           sh "npm install"
           }
       }
   }
}
}