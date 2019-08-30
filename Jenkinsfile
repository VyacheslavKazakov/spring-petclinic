node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git('https://github.com/VyacheslavKazakov/spring-petclinic.git')
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.
      mvnHome = '.'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=${mvnHome}"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/mvnw" verify'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      [ $class: 'JacocoPublisher' ]
      archiveArtifacts 'target/*.jar'
   }
}
