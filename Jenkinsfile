pipeline {
  agent any
  stages {
    stage('Clone Code') {
      steps {
        git 'https://github.com/<your-username>/<your-repo-name>.git'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t <dockerhub-username>/myapp .'
      }
    }
    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
          sh 'docker push <dockerhub-username>/myapp'
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
  }
}
