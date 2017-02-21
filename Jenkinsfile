pipeline {
  agent any

  environment {
    IMAGE_NAME = 'prydonius/node-todo'
    RELEASE_NAME = 'test'
    HELM_URL = 'https://storage.googleapis.com/kubernetes-helm'
    HELM_TARBALL = 'helm-v2.2.0-linux-amd64.tar.gz'
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

        sh '''
          curl -O $HELM_URL/$HELM_TARBALL
          tar xzfv $HELM_TARBALL -C /home/jenkins && rm $HELM_TARBALL
          PATH=/home/jenkins/linux-amd64/:$PATH
          helm init --client-only

          helm dependencies build ./helm/todo
          helm upgrade $RELEASE_NAME ./helm/todo --set image.tag=$BUILD_ID
        '''
      }
    }
  }
}
