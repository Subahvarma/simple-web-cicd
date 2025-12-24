pipeline {
  agent any

  environment {
    DOCKER_IMAGE = "subhadra777/cicd"
  }

  stages {

    stage('Clone Code') {
      steps {
        git 'https://github.com/subahvarma/simple-web-cicd.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $DOCKER_IMAGE:latest .'
      }
    }

    stage('Push Image to Docker Hub') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'docker',
          usernameVariable: 'subhadra777',
          passwordVariable: 'Subbu@123'
        )]) {
          sh '''
          echo $PASS | docker login -u $USER --password-stdin
          docker push $DOCKER_IMAGE:latest
          '''
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh '''
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
        '''
      }
    }
  }
}

