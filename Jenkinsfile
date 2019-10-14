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
        sh 'mvn clean sonar:sonar install'
        )
      }
    }    
  }
}
