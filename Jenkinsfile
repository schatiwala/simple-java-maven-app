pipeline {
  agent any
  stages {
    stage('Source') { // Get code
      steps {
        // get code from our Git repository
        git 'https://github.com/schatiwala/simple-java-maven-app'
      }
    }
    stage('Compile') { // Compile and do unit testing
      steps {
        // run mvn to execute compile and unit testing
        sh 'mvn clean install'
      }
    }
  }
}
