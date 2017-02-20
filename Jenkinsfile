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
        echo 'TODO: add tests'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub',
          usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {

          echo '${env.DOCKER_USERNAME}'
        }
      }
    }
  }
}
