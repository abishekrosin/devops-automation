pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abishekrosin/devops-automation']]]) 
                bat 'mvn clean package -x'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t abishekrosin/devops-integration .'
                }
            }
        }
        stage('Push Image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        bat 'docker login -u rosin -p %dockerhubpwd%'
                    }
                    bat 'docker push abishekrosin/devops-integration'
                }
            }
        }
    }
}
