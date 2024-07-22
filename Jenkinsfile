pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abishekrosin/devops-automation']]]) 
                bat 'mvn clean package'
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
                    
                        bat 'docker login -u rosin -p rosin007'
                    }
                    bat 'docker push abishekrosin/devops-integration'
                }
            }
        }
    }
}
