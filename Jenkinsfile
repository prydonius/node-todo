pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Testing Docker...'
        sh 'docker build -t prydonius/node-todo .'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing..'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying....'
      }
    }
  }
}
