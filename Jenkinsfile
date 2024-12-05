@Library("Shared") _
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
                 sh "docker compose down && docker compose up -d"
            }
            
        }
    }
}
