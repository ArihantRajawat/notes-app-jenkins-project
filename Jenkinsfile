pipeline {
    
    agent any
    
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/ArihantRajawat/notes-app-jenkins-project.git", branch: "main"
                echo "Aaj toh LinkedIn Post bannta hai "
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t notes-app-jenkins:latest"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials(
                    [usernamePassword(
                        credentialsId:"dockerCreds",
                        passwordVariable:"dockerHubPass", 
                        usernameVariable:"dockerHubUser"
                        )
                    ]
                ){
                sh "docker image tag notes-app-jenkins:latest ${env.dockerHubUser}/notes-app-jenkins:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app-jenkins:latest"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
