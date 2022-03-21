pipeline {
    
    agent any
    
    tools{
        maven 'maven3.8.4'
    }
    
    stages{
        
        stage('git clone'){
            steps{
            
            git credentialsId: 'GIT-HUB-CREDENTIALS', url: 'https://github.com/bpavani1992/docker_compose_handson.git'
            }
        }
        stage('maven package'){
            steps{
            
            sh "mvn clean package"
            }

        }
        stage('docker build image'){
            steps{
                
            sh "docker build -t bpavani/mavenapp:1 ."
            }
        }

        stage('docker login'){ 
            steps{
            
            withCredentials([string(credentialsId: 'Docker_hub_password', variable: 'DOCKER_HUB_PASSWORD')]){

                sh "docker login -u bpavani -p ${DOCKER_HUB_PASSWORD}"
            }

            sh "docker push bpavani/mavenapp:1"
            }
            
        }
        stage('deploy to server'){
            steps{
        sshagent(['ssh_credentials_docker_compose']) {
            sh " docker-compose up"
        }
            }
        }
  
              
        }
    }
