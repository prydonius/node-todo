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

          sh '''
            docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
            docker tag prydonius/node-todo:latest prydonius/node-todo:$BUILD_ID
            docker push prydonius/node-todo:$BUILD_ID
          '''
        }
      }
    }
  }
}
