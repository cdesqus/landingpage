properties([pipelineTriggers([githubPush()])]) 
pipeline {
    agent any
    stages {
        stage('Test') {
        agent { label "agent" } // Define mau running di agent yang mana
            steps {
              // Test menggunakan Sonarqube
                script { echo "Begin Testing Using Sonarqube" 
                def scannerHome = tool 'sonarqube' ; //sonarqube by Global Tools Configuration
                withSonarQubeEnv('sonarqube') {  //sonarqube by Endpoint Server Sonarqube
                sh "${scannerHome}/bin/sonar-scanner"}
                } 
              }
            
            }
        stage('Build') {
        agent { label "agent" } // Define mau running di agent yang mana
            steps {
              // Build Image
                script { echo "Begin Build"
                if (env.BRANCH_NAME == "dev")
                
                { 
                sh "docker build -t harjay88/landingpage:dev-$BUILD_NUMBER . "
                sh "docker push harjay88/landingpage:dev-$BUILD_NUMBER"

                }else{ 
                sh "docker build -t harjay88/landingpage:master-$BUILD_NUMBER . "
                sh "docker push harjay88/landingpage:master-$BUILD_NUMBER"
                
                }
                
                
                }
                
              }
            }
        stage('Deploy') {
        agent { label "agent" }  // Define mau running di agent yang mana
            steps {
              // Deploy to Kubernetes
                script { echo "Begin to Deploy" 
                sh "kubectl set image deployment/landingpage landingpage=harjay88/landingpage:dev-$BUILD_NUMBER -n landingpage"
                }
            }
          }
        }
      }