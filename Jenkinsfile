pipeline{
    agent any
    
    stages {
        stage("clone"){
          steps{
              echo "cloing the code"
             git url:"https://github.com/MddMohideen/django-notes-app.git", branch:"main"
          } 
        }
            stage("build"){
              steps{
                echo "building the image"
                 sh "docker build -t mynotes-app ."
                }
            }
        stage("push"){
            steps{
            echo "pushing the image to dockerhub"
                 withCredentials([usernamePassword(credentialsId:"Dockerhub",passwordVariable:'DockerhubPass',usernameVariable:'DockerhubUser')]){
                 sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPass}"
                 sh "docker tag mynotes-app  ${env.dockerHubUser}/today-apps"
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                 sh "docker push ${env.dockerHubUser}/today-apps"
                    
                    
                }
            }
        }
          
        stage("deploy"){
            steps{
            echo "deploying the container"
            sh "docker-compose down && docker-compose up -d"
            }
        }
    }
    
}

