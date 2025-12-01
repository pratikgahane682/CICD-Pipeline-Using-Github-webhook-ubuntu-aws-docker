pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nest-image"
        EMAIL: "pratikgahane619@gmail.com"
        PORT: "3000"
       
    }

    stages {

        stage('Clone repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/pratikgahane682/CICD-Pipeline-Using-Github-webhook-ubuntu-aws-docker'
            }
        }

    
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop and remove previous container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || 
                true
                docker rm CONTAINER_NAME || 
                true


                '''
            }
        }
        stage('Docker container run') {
            steps {
                sh '''
                docker run -d -p ${PORT}:$(PORT) 
                --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }


        stage('Send email notification') {
            steps {
                email text(
                    subject: "NestJS app deploy successfully on EC2",
                    body: "Our app is ready to use /NestJS is DEPLOYED! http://3.110.180.218:${PORT}/",
                    to: "${EMAIL}"
        
                )
            }
        }

}
