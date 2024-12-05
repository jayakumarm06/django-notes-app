pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t note-app-test-new"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag note-app-test-new ${env.dockerHubUser}/note-app-test-new:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/note-app-test-new:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}@Library("Shared") _
pipeline{
    
    agent{label "vinod"}
    
    stages{
        stage('Hello'){
            steps{
                script{
                    hello()
                }
            }
        }
            
        stage("code"){
            steps{
                script{
                  clone("https://github.com/jayakumarm06/django-notes-app.git","master")
                }
                
            }
            
        }
        stage('Build'){
            steps{
                script{
                    docker_build("notes-app","latest","jaikumarm06")
                }
                
            }
            
        }
        stage('Push to DockerHUB'){
            steps{
                script{
                    docker_push("notes-app","latest","jaikumarm06")
                }
                    
            }
                
        }
        stage("Deploy"){
            steps{
                 echo "This is Deploy the code"
                 //sh "docker run -d -p 8000:8000 notes-app:latest"
                 sh "docker compose up -d"
            }
            
        }
    }
}
