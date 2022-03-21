pipeline {
    
    agent any
    
    stages{
        
        stage(git clone){
            
            git credentialsId: 'GIT-HUB-CREDENTIALS', url: 'https://github.com/bpavani1992/docker_compose_handson.git'
        }
        stage(maven package){
            
            sh mvn clean package

        }
        stage(docker build image){
            sh "docker build -t bpavani/mavenapp:1 ."
        }

        stage(docker login){ 
            
            withCredentials([string(credentialsId: 'Docker_hub_password', variable: 'DOCKER_HUB_PASSWORD')]){

                sh "docker login -u bpavani -p ${DOCKER_HUB_PASSWORD}"
            }

            sh docker push bpavani/mavenapp:1
        }
        

        }
    }
