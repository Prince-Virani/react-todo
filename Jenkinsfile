pipeline {
    agent any
    stages {
        stage('clone the code') {
            steps {
                echo "cloning the code"
                git url:"https://github.com/devOps-pri/react-todo.git", branch: "main"
            }
        }
        stage(build the image){
            steps{
                echo "building the images"
                sh "docker build -t myreact-app ."
            }

        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag myreact-app ${env.dockerHubUser}/myreact-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/myreact-app:latest"
                }
                
            }
    
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"

            }
        }

}

}
