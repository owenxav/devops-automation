pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage("Build Maven"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/owenxav/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                 sh 'docker build -t owenagboje/devops-integration .'
                }
            }
        }
        stage('Push Image to Hub'){
            steps{
                script{
                 withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                 sh 'docker login -u owenagboje -p ${dockerhubpwd}'
}
                 sh 'docker push owenagboje/devops-integration'
                }
            }
        }
    }
}
