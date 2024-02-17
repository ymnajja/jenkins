pipeline {
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/LondheShubham153/node-todo-cicd.git", branch: "master"
            }
        }
        stage ("Build"){
            steps{
                sh "npm install"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"Youssef@mnajja123",usernameVariable:"youffes")]){
                    sh "docker tag node-app-test-new ${DOCKER_HUB_USER}/node-app-test-new:latest"
                    sh "docker login -u ${DOCKER_HUB_USER} -p ${DOCKER_HUB_PASS}"
                    sh "docker push ${DOCKER_HUB_USER}/node-app-test-new:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
