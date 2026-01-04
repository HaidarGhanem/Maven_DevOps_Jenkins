pipeline {
    agent any 
    tools {
        maven "maven-3.9"
    }
    stages {
        stage("build jar"){
            steps{
                script{
                    echo "building application ..."
                    sh "mvn package"
                }
            }
        }
        stage("build image"){
            steps{
                withCredentials([
                    usernamePassword(credentialsId:'docker-hub',usernameVariable:'USER',passwordVariable:'PWD')
                ]){
                    sh "docker build -t $USER/demo-maven:1.0 ."
                    sh "echo $PWD | docker login -u $USER --password-stdin"
                    sh "docker push $USER/demo-maven:1.0"
                }
                }
                script{
                    echo "building docker image ..."
                    sh "mvn package"
                }
            }
        }
        stage("deploy"){
            steps{
                script{
                    echo "deploying application ..."
                }
            }
        }
    }
