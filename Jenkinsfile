pipeline{
    agent any
    stages {
        stage('Build app'){
            steps{
                script{
                    echo "Building the application.."
                }
            }
        }
        stage('Build image'){
            steps{
                script{
                    echo "Building the docker image.."
                }
            }
        }
        stage('Deploy'){
            steps{
                script{
                    echo "Deploying docker image.."
                }
            }
        }
    }
}