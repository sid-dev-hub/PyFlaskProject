pipeline {
    agent any
    environment {
        IMAGE_NAME = 'sidsalakki14/ci-cd-demo'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sid-dev-hub/PyFlaskProject.git'
            }
        }

        stage('Code Quality') {
            steps {
                sh 'sonar-scanner'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push $IMAGE_NAME:$BUILD_NUMBER
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig([credentialsId: 'kubeconfig']) {
                    sh 'helm upgrade --install ci-cd-app helm-chart/ --set image.tag=$BUILD_NUMBER'
                }
            }
        }
    }
}
