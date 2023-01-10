pipeline{
    agent any
    environment{
        DOCKER_SERVER = "073047198118.dkr.ecr.ap-south-1.amazonaws.com"
        DOCKER_REPO = "073047198118.dkr.ecr.ap-south-1.amazonaws.com/django-todo"
        IMAGE_NAME = "${DOCKER_REPO}:${BUILD_NUMBER}"
    }
    stages{
        stage("Docker build & push"){
            steps{
                script{
                    echo "build & Push the image on dockerhub.!!"
                    sh "docker build -t ${env.IMAGE_NAME} ."
                    withCredentials([usernamePassword(credentialsId: 'ECR_Credentials',passwordVariable: 'PWD',usernameVariable: 'USER')]){
                    sh "docker login -u ${env.USER} -p ${env.PWD} ${env.DOCKER_SERVER}"
                    sh "docker push ${env.IMAGE_NAME}"
                    }   
                }
            }
        }
        stage("Cleaning up docker images"){
            steps{
                script{
                    sh "docker images"
                    sh "docker rmi -f ${IMAGE_NAME}"
                    sh "docker images"  
                }
            }
        }
        stage("Deploy image"){
            environment {
                APP_NAME = 'django-todo'
            }
            steps{
                script{
                    echo 'Deploying docker image...'
                    sh 'envsubst < kubernetes/deployment.yaml | kubectl apply -f -'  
                    sh 'envsubst < kubernetes/service.yaml | kubectl apply -f -'
                }
            }
        }
    }
}

// envsubst --> apt install gettext-base (package which includes envsubst tool)