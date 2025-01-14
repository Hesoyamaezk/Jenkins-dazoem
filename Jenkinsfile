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
            agent any
            steps {
                echo 'Building the app'
            }
        }

        stage('Test') {
            agent any
            steps {
                echo 'Testing the app'
            }
        }

        stage('Deploy') {
            agent any
            steps {
                echo 'Deploying the app'
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
