pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yourrepo/webpage.git'  // web page code
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mywebpage:latest .'
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker tag mywebpage:latest mydockerhubuser/mywebpage:latest'
                sh 'docker push mydockerhubuser/mywebpage:latest'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig([credentialsId: 'k8s-cred']) {
                    sh 'kubectl apply -f k8s-deployment.yml'
                }
            }
        }
    }
}
