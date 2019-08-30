pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git(url: 'https://github.com/VyacheslavKazakov/spring-petclinic.git', branch: '*/master', changelog: true, poll: true)
        sh './mvnw verify'
        junit(testResults: '**/target/surefire-reports/TEST-*.xml', allowEmptyResults: true)
        jacoco()
      }
    }
  }
}