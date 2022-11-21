pipeline {
    agent any

    stages{
            
        stage('Build'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Raunak0604/TO-DO-App-Deploy']]])                    
            }
        }
        
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t rabbit0604/todoapp .'
                    sh 'if docker images -f "dangling=true" | grep ago --quiet;'
                    sh 'then docker rmi -f $(docker images -f "dangling=true" -q)'
                    sh 'fi'
                    
                }
            }
        }
        
        stage('Push image to Hub'){
            steps{
                script{
                        withCredentials([string(credentialsId: 'DockerHub-PWD', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u rabbit0604 -p ${dockerhubpwd}'
                    }
                    sh 'docker push rabbit0604/todoapp'
                }
            }
        }

    }
    
}
