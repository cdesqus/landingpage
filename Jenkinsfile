pipeline {
agent any
stages {
stage('Build') {
  agent { label "agent1" }
steps {
  //
  script { echo "Build" }
}
}
stage('Test') {
  agent { label "agent1" }
steps {
//
  script { echo "Test" }
}
}
stage('Deploy') {
  agent { label "agent1" }
steps {
//
  script { echo "Deploy" }
}
}
}
}
