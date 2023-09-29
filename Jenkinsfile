pipeline {
  agent any
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

        stage('Upload Artifact') {
          steps {
            mail(subject: 'UploadDone', body: 'Hello World', from: 'rjoshi@adobe.com', to: 'rjoshi@adobe.com', replyTo: 'rjoshi@adobe.com')
          }
        }

      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}