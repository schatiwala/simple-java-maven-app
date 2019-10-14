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
		stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "Artifactory4.15.0",
                    url: "http://localhost:8081",
                    credentialsId: "artifactory"
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "Artifactory4.15.0",
                    releaseRepo: "/artifactory/webapp/#/admin/repository/local/libs-release-local/libs-release-local",
                    snapshotRepo: "/artifactory/webapp/#/admin/repository/local/libs-release-local/libs-snapshot-local"
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "Artifactory4.15.0",
                    releaseRepo: "/artifactory/webapp/#/admin/repository/local/libs-release-local/libs-release-local",
                    snapshotRepo: "/artifactory/webapp/#/admin/repository/local/libs-release-local/libs-snapshot-local"
                )
            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'maven3', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Artifactory4.15.0"
                )
            }
      }    
  }
}
