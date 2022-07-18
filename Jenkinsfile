properties([pipelineTriggers([githubPush()])]) 
pipeline {
    agent any
    stages {
        stage('Build') {
        agent { label "Agent" }
            steps {
              //
                script { echo "Build"
                if (env.BRANCH_NAME == "dev")
                
                { 
                sh "docker build -t harjay88/landingpage_test:dev-$BUILD_NUMBER . "
                sh "docker push harjay88/landingpage_test:dev-$BUILD_NUMBER"

                }else{ 
                sh "docker build -t harjay88/landingpage_test:master-$BUILD_NUMBER . "
                sh "docker push harjay88/landingpage_test:master-$BUILD_NUMBER"
                
                }
                
                
                }
                
              }
            }
        stage('Test') {
        agent { label "Agent" }
            steps {
              //
                script { echo "Test" }
              }
            }
        stage('Deploy') {
        agent { label "Agent" }
            steps {
              //
                script { echo "Deploy3" }
            }
          }
        }
      }
