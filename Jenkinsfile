pipeline {
  agent none

  environment {
    IMAGE_NAME = 'prydonius/node-todo'
  }

  stages {
    stage('Build') {
      agent any

      steps {
        checkout scm
        sh 'docker build -t $IMAGE_NAME:$BUILD_ID .'
      }
    }
    stage('Test') {
      agent any

      steps {
        echo 'TODO: add tests'
      }
    }
   
    stage('Staging Deployment') {
      agent any

      when {
        expression { env.BRANCH_NAME == 'master' }
      }

      environment {
        RELEASE_NAME = 'todos-staging'
        SERVER_HOST = 'todos.staging.k8s.prydoni.us'
      }

      steps {
        sh '''
          . ./helm/helm-init.sh
          helm dependencies build ./helm/todo
          helm upgrade --install --namespace staging $RELEASE_NAME ./helm/todo --set image.tag=$BUILD_ID,ingress.host=$SERVER_HOST
        '''
      }
    }
    stage('Deploy to Production?') {
      when {
        expression { env.BRANCH_NAME == 'master' }
      }

      steps {
        // Prevent any older builds from deploying to production
        milestone(1)
        input 'Deploy to Production?'
        milestone(2)
      }
    }
    stage('Production Deployment') {
      agent any

      when {
        expression { env.BRANCH_NAME == 'master' }
      }

      environment {
        RELEASE_NAME = 'todos-production'
        SERVER_HOST = 'todos.k8s.prydoni.us'
      }

      steps {
        sh '''
          . ./helm/helm-init.sh
          helm dependencies build ./helm/todo
          helm upgrade --install --namespace production $RELEASE_NAME ./helm/todo --set image.tag=$BUILD_ID,ingress.host=$SERVER_HOST
        '''
      }
    }
  }
}
