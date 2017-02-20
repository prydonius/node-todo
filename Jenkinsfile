pipeline {
  agent any

  environment {
    IMAGE_NAME = 'prydonius/node-todo'
  }

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$BUILD_ID .'
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
            docker push $IMAGE_NAME:$BUILD_ID
          '''
        }
      }
    }
  }
}
