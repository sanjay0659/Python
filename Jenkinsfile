pipeline {
    agent any
    environment { 
        IMAGE_NAME = "botadmin/${env.JOB_NAME}"
        IMAGE_TAG =  "${IMAGE_NAME}:${env.GIT_COMMIT.take(2)}"
    }
    stages {
        stage ('login to docker hub') {
            steps {
                withCredentials([usernamePassword(credentialsId:'docker_creds', usernameVariable: 'username', passwordVariable:'password')]){
                    sh 'docker login -u ${username} -p ${password}'
                }
            }
            
        }
        stage ('Docker build') {
            steps {
                sh 'docker build -t ${IMAGE_TAG} .'
                echo "docker build is success"

            }
        }
        stage ('Docker push') {
            steps {
                sh 'docker push ${IMAGE_TAG}'
                echo "image push is successful"
            }
        }
    }
}