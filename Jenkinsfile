pipeline {
  agent any

  environment {
    DOCKER_HUB = 'aravind310730/my-app'
    IMAGE_TAG = "${env.BUILD_NUMBER}"
    SONARQUBE_SERVER = 'SonarQube'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/aravind30122003/CI-CD-PROJECT.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${DOCKER_HUB}:${IMAGE_TAG}")
        }
      }
    }

    stage('Unit Tests') {
      steps {
        sh 'pytest tests/' // Optional: If you have tests
      }
    }

    stage('SonarQube Scan') {
      steps {
        withSonarQubeEnv(SONARQUBE_SERVER) {
          sh 'sonar-scanner'
        }
      }
    }

    stage('Trivy Scan') {
      steps {
        sh "trivy image --exit-code 1 --severity CRITICAL ${DOCKER_HUB}:${IMAGE_TAG}"
      }
    }

    stage('Push to Docker Hub') {
      steps {
        withDockerRegistry([credentialsId: 'dockerhub-cred', url: '']) {
          sh "docker push ${DOCKER_HUB}:${IMAGE_TAG}"
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh """
          helm upgrade --install my-webapp ./helm \
          --set image.repository=${DOCKER_HUB} \
          --set image.tag=${IMAGE_TAG}
        """
      }
    }
  }
}