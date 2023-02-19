pipeline {
  agent any
  tools {
    maven 'maven 3.9.0'
  }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
  stages {
    stage('Build') {
      steps {
        sh './mvnw clean install'
      }
    }
    stage('Upload to Artifactory') {
      agent {
        docker {
          image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0'
          reuseNode true
        }
      }
      steps {
        sh 'jfrog rt upload --url http://http://localhost:8082/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/example-project-1.0.0-SNAPSHOT.jar libs-snapshot-local/'
      }
    }
  }
}