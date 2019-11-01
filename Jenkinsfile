pipeline {
  agent any
      tools {
        jdk 'JDK1.8'
        maven 'maven3'
      }
  stages {
    stage('Source') { // Get code
      steps {
        // get code from our Git repository
        git 'https://github.com/schatiwala/simple-java-maven-app'
      }
    }
    stage ('compile and SonarQube Testing') {
      steps {
        sh 'mvn clean sonar:sonar compile'
      }
    }
    stage("Quality Gate"){
      steps {
        timeout(time: 2, unit: 'MINUTES') {
          def qg = waitForQualityGate()
          if (qg.status != 'OK') {
            error "Pipeline aborted due to quality gate failure: ${qg.status}"
          }
        }
      } 
    }        
    stage ('Test state') {
      steps {
        sh 'mvn test'
      }
    }
    stage ('Deploy') {
      steps {
        sh 'mvn install'
      }
    }
  }
}
