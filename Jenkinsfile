pipeline {
    agent any 
    
    tools {
        maven "maven-3.9"
    }
    
    stages {
        stage("Build Jar") {
            steps {
                script {
                    echo "Building application JAR..."
                    sh "mvn clean package"
                }
            }
        }

        stage("Build & Push Image") {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USER', passwordVariable: 'PWD')
                ]) {
                    script {
                        echo "Building Docker image..."
                        sh "docker build -t ${USER}/demo-maven:1.0 ."
                        
                        echo "Logging into Docker Hub..."
                        sh "echo ${PWD} | docker login -u ${USER} --password-stdin"
                        
                        echo "Pushing image..."
                        sh "docker push ${USER}/demo-maven:1.0"
                    }
                }
            }
        }

        stage("Deploy") {
            steps {
                script {
                    echo "Deploying application..."
                }
            }
        }
    }
}