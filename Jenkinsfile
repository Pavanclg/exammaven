pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t exam .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl create deployment exam-app --image=exam-app'
                sh 'kubectl expose deployment exam-app --type=NodePort --port=8080'
            }
        }
    }
}
