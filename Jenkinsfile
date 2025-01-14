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
        stage('Prepare') {
            environment {
                APP = credentials('dazoem_rahasia')
              }
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
                echo 'Preparing ....'
                echo 'Author : ${env.AUTHOR} and Email : ${env.EMAIL}'
                echo 'Start Job : ${env.JOB_NAME}'
                echo 'Start Build : ${env.BUILD_NUMBER}'
                echo 'Branch : ${env.BRANCH_NAME}'
                echo 'App user : ${APP_USR}'
                echo 'Preparation done!'
            }
        }
        stage('Build') {
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
              script {
                  for (int i = 0; i < 5; i++) {
                    echo "Hello World ${i}"
                  }
                }
                echo "Building with author: ${env.AUTHOR} and email: ${env.EMAIL}"
                sh './mvnw clean compile test-compile'
                echo 'Build done!'
            }
        }
        stage('Test') {
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
              script {
                  def data = [
                    'firstName' : 'Ahmad',
                    'lastName' : 'Wizam',
                  ]
                  writeJSON file: 'data.json', json: data
                } 
                echo 'Testing ....'
                sh './mvnw test'
                echo 'Testing done!'
            }
        }
        stage('Deploy') {
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
                echo 'Deploying ....'
                echo 'Deploying done!'
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




