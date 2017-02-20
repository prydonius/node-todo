pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Testing Docker...'
        sh 'sleep 3600'
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
