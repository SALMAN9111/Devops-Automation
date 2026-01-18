pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SALMAN9111/Devops-Automation.git']])
               bat 'mvn clean install'
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhub-pwd')]) {
                    bat "echo %dockerhub-pwd% | docker login -u sayedsalman --password-stdin"
                }
            }
        }
        stage('Build & Push Docker Image') {
            steps {
                bat "docker build -t sayedsalman/devops-integration:latest ."
                bat "docker push sayedsalman/devops-integration:latest"
            }
        }
    }
}