env.DOCKER_REGISTRY = 'ikhsannugs'
env.DOCKER_IMAGE_NAME = 'test-land'
node('master') {
    stage('Git Pull') {
          checkout scm
    }
      stage('Build Docker Image') {
        sh "docker build -t $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER} ."   
    }
      stage('Push Docker Image to Dockerhub') {
          sh "docker push $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER}"
    }
          stage('Deploy to Server') {
          sh "kubctl apply -f deployment"
    }
    stage('Remove Docker Image') {
        sh "docker rmi $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME:${BUILD_NUMBER}"   
    }
}
