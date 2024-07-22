pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abishekrosin/devops-automation']]]) // Removed the extra 'z'
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t abishekrosin/devops-integration .'
                }
            }
        }
        stage('Push Image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u rosin -p ${dockerhubpwd}'
                    }
                    sh 'docker push abishekrosin/devops-integration'
                }
            }
        }
    }
}
