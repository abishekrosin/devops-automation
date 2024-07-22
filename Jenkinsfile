pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abishekrosin/devops-automation']]])
                bat 'mvn clean package' // Use 'sh' if Jenkins is running on Unix-like systems
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t abishekrosin/devops-integration .' // Use 'sh' if Jenkins is running on Unix-like systems
                }
            }
        }
        stage('Push Image to Hub') {
            steps {
                script {
                    bat 'docker login' // No need for username and password since we're using the credential store
                    bat 'docker push abishekrosin/devops-integration' // Use 'sh' if Jenkins is running on Unix-like systems
                }
            }
        }
    }
}
