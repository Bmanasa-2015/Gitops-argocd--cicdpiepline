pipeline {
    agent any

    environment {
        IMAGE_NAME = "manasabolla/flask-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        GITOPS_REPO = "https://github.com/Bmanasa-2015/Gitops-argocd--cicdpiepline.git"
    }

    stages {

        stage('Checkout App Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Bmanasa-2015/Gitops-argocd--cicdpiepline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                """
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh """
                    echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }

        stage('Update GitOps Repo') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'github-creds',
                        usernameVariable: 'GIT_USER',
                        passwordVariable: 'GIT_TOKEN'
                    )
                ]) {
                    sh """
                    rm -rf gitops

                    git clone https://\$GIT_USER:\$GIT_TOKEN@github.com/Bmanasa-2015/Gitops-argocd-cicdpiepline.git gitops

                    cd gitops

                    sed -i 's|image: .*|image: ${IMAGE_NAME}:${IMAGE_TAG}|g' deployment.yaml

                    # git config user.email "jenkins@example.com"
                    # git config user.name "Jenkins"

                    git add deployment.yaml
                    git commit -m "Update image tag to ${IMAGE_TAG}" || true

                    git push origin main
                    """
                }
            }
        }
    }
}
