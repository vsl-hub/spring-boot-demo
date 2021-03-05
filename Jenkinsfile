node ('Slave2'){
   def mvnHome
   stage('Prepare') {
      git 'https://github.com/vsl-hub/spring-boot-demo.git'
      mvnHome = tool 'maven'
   }
   stage('Compile') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean compile"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean compile/)
      }
   }
   stage('Code Review') {
   if (isUnix()) {
   sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
   } else {
   bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
   }
 }
   stage('Unit Testing') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
   stage('Integration Test') {
     if (isUnix()) {
        sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean verify"
     } else {
        bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean verify/)
     }
   }
}
