pipeline {

    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {

        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t springboot-k8s-demo .'
            }
        }

        stage('Load Image') {
            steps {
                bat 'minikube image load springboot-k8s-demo'
            }
        }

        stage('Deploy') {
            steps {
                bat 'kubectl apply -f k8s/'
            }
        }

        stage('Verify') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }

    }

}