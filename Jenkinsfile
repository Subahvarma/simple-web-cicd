pipeline {
  agent any

  environment {
    DOCKER_IMAGE = "subhadra777/cicd"
    GIT_REPO_NAME = "simple-web-cicd"
    GIT_USERNAME = "subahvarma"
    BRANCH = "master"
  }

  stages {

    stage('Clone Code') {
      steps {
        git branch: "${BRANCH}", credentialsId: 'git_token', url: 'https://github.com/Subahvarma/simple-web-cicd.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $DOCKER_IMAGE:latest .'
      }
    }

    stage('Push Image to Docker Hub') {
      steps {
    
          withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                      
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

