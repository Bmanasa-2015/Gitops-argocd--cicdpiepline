pipeline {
 agent any
 environment {
  IMAGE='yourdockerhub/flask-app'
  TAG="${BUILD_NUMBER}"
 }
 stages {
  stage('Checkout'){steps{checkout scm}}
  stage('Build'){steps{sh 'docker build -t $IMAGE:$TAG app/'}}
  stage('Push'){steps{echo 'Configure docker credentials';}}
  stage('Update GitOps Repo'){
   steps{echo 'Update deployment image tag in GitOps repo'}
  }
 }
}
