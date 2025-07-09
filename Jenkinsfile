pipeline {
  agent any

  environment {
    IMAGE_NAME = 'amisha0704/python-app'  // ⬅️ Replace with your Docker Hub repo name
    IMAGE_TAG = 'latest'
  }

  stages {
    stage('Checkout') {
      steps {
        // Jenkins will checkout the repo automatically in Pipeline jobs
        echo "Checking out source code..."
      }
    }

    stage('Build Docker Image') {
      steps {
        echo "Building Docker image..."
        sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
      }
    }

    stage('Push Docker Image') {
      steps {
        echo "Pushing Docker image to Docker Hub..."
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub',           // ⬅️ Must match Jenkins credentials ID
          usernameVariable: 'DOCKER_USER',
          passwordVariable: 'DOCKER_PASS'
        )]) {
          sh '''
            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
            docker push $IMAGE_NAME:$IMAGE_TAG
          '''
        }
      }
    }
  }

  post {
    success {
      echo "✅ Docker image pushed: $IMAGE_NA_
