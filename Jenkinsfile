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
    stage ('Build and SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonar') {
          sh 'mvn clean package sonar:sonar'
        }  
      }
    }
    stage("Quality Gate"){
      steps {
        timeout(time: 1, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
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
