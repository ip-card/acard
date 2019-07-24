@Library('pipeline-library-demo')_

def sayHello1(String name = 'human') {
  echo "Hello, ${name}."
  echo "Hello, ${name}."
}
node('maven-label') {
   def mvnHome
   
   stage('shared-lib-ex'){
      sayHello2 'IntelliPath'
   }
   stage('shared-lib-ex'){
      sayHello 'IntelliPath'
   }
   stage('Preparation') { 
      
      git 'https://github.com/ip-card/acard.git'
              
      mvnHome = tool 'maven-3.6.1'
   }
   stage('Build') {
      
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
