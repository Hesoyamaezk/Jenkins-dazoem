pipeline {
    agent none

    environment {
        AUTHOR = 'Ahmad wizam'
        EMAIL = 'Ahmadwizam12@gmail.com'
    }

    triggers {
        pollSCM('*/5 * * * *')
      }

    stages {
      stage('Build') {
          agent {
              node {
                  label 'linux && java11'
              }
            }
        }
      stage('Test') {
          agent {
              node {
                  label 'linux && java11'
              }
            }
        }
      stage('Deploy') {
          agent {
              node {
                  label 'linux && java11'
              }
            }
        }
    }

    post {
      always {
        echo 'This will always run'
      }
      success {
        echo 'This will run only if successful'
      }
      failure {
        echo 'This will run only if failed'
      }
      cleanup {
        echo 'This will always run'
      }
    }
}
