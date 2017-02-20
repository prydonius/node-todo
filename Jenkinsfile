pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Testing Docker..'
        sh 'docker version'
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
