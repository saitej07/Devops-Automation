pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [],  userRemoteConfigs: [[url: 'https://github.com/saitej07/Devops-Automation']]])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t saitej150/devops-integration .'
                }
            }
        }
        stage('Push Image to Hub') {
            steps {
                script {
                  withCredentials([string(credentialsId: 'saitej150', variable: 'dockerhub')]) {
                  bat 'docker login -u saitej150 -p ${dockerhub}'
}

                  bat 'docker push saitej150/devops-integration'
                }
            }
        }
    }
}
