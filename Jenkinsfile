pipeline {
agent any
tools {nodejs "node-env"}
stages {
 stage("Code Checkout from GitHub") {
  steps {
  checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'a6f4081c-63d6-441b-b8de-c99fd34f8502', url: 'https://github.com/coderbpl/node-js-getting-started.git']]])
  }
 }
   stage('Code Quality Check via SonarQube') {
   steps {
       script {
       def scannerHome = tool 'sonarqube';
           withSonarQubeEnv("sonarqube-container") {
            nodejs(nodeJSInstallationName: 'node-env'){
           sh "npm install"
             sh "npm run sonar"
           }
               }
           }
       }
   }
   
}
}
