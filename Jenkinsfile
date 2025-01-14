pipeline {
    agent none

    environment {
        AUTHOR = 'Ahmad wizam'
        EMAIL = 'Ahmadwizam12@gmail.com'
    }

//    triggers {
//      pollSCM('*/5 * * * *')
//    }

    parameters {
      string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
      text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
      booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
      choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
      password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {

        stages('OS Setup'){
            matrix {
                axes {
                    axis {
                        name 'OS'
                        values 'linux', 'windows'
                    }
                    axis {
                        name 'ARC'
                        values 'x86', 'x64'
                    }
                }
                stages {
                    stage('OS Setup'){
                        agent {
                            node 'linux && java11'
                        }
                    }
                    steps {
                        echo "Setup ${OS} ${ARC}"
                    }
                }
           }
        }
      


        stage('Preparation'){
            parallel {
                stage('Prepare Java') {
                    agent {
                        node {
                            label 'linux && java11'
                        }
                    }
                    steps {
                        echo 'Preparing Java ....'
                        echo 'Java Preparation done!'
                        sleep 5
                    }
                }
                stage('Prepare Maven') {
                    agent {
                        node {
                            label 'linux && java11'
                        }
                    }
                    steps {
                        echo 'Preparing Maven ....'
                        echo 'Maven Preparation done!'
                        sleep 5
                    }
                }
            }
          }

        stage('Parameters'){
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "Description : ${params.DESCRIPTION}"
                echo "Deploy : ${params.DEPLOY}"
                echo "Social Media : ${params.SOCIAL_MEDIA}"
                echo "Secret : ${params.SECRET}"
            }
        }
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
                echo "Author : ${env.AUTHOR} and Email : ${env.EMAIL}"
                echo "Start Job : ${env.JOB_NAME}"
                echo "Start Build : ${env.BUILD_NUMBER}"
                echo "Branch : ${env.BRANCH_NAME}"
                echo "App user : ${APP_USR}"
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
            input {
                message 'Do you want to deploy?'
                ok 'Yes, of course'
                submitter 'Ahmad Wizam'
                parameters {
                    choice(name: 'TARGET_ENV', choices: ['DEV', 'STAGING', 'PRODUCTION'], description: 'We will deploy to?')
                  }
            }
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
                echo "Deploying to ${TARGET_ENV}"
                echo 'Deploying done!'
            }
        }
        stage('Release') {
            when {
              expression {
                  return params.DEPLOY;
              }
            }
            agent {
                node {
                    label 'linux && java11'
                }
            }
            steps {
                echo 'Releasing ....'
                echo 'Releasing done!'
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




