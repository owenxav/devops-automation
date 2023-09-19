pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("Build Maven") {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/owenxav/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t owenagboje/devops-integration .'
                }
            }
        }
        stage('Push Image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerpwd')]) {
                        bat "docker login -u owenagboje -p \"${dockerpwd}\""
                    }
                    bat 'docker push owenagboje/devops-integration'
                }
            }
        }
    }
}
