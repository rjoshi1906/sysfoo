pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'compile maven app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            echo 'test maven app'
            sh 'mvn clean test'
          }
        }

        stage('Integration Test') {
          steps {
            sleep 10
          }
        }

        stage('Code Coverage') {
          steps {
            sleep 3
          }
        }

      }
    }

    stage('package') {
      parallel {
        stage('package') {
          steps {
            echo 'package maven app'
            sh 'mvn package -DskipTests'
            archiveArtifacts 'target/*.war'
          }
        }

        stage('UploadArtifact') {
          steps {
            sleep 2
          }
        }

      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}