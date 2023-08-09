pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                echo "checkout code"
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/LondheShubham153/django-notes-app.git']])
            }
        
        }
        stage('build image') {
            steps {
                echo "building image"
                sh 'docker build -t konark111/cicd2 .'
            }
        
        }
        stage('push image to dockerhub'){
            steps{
                echo "push image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push konark111/cicd2"
            }
            }
        }
        stage('deploy container'){
            steps{
                echo "deploy container to instance"
                sh "docker-compose down && docker-compose -d up"


            }
        }
    }
}
