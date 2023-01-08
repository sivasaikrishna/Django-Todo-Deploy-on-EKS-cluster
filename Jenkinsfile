pipline{
    agent any
    stages {
        stage('build app'){
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
        stage('deploy'){
            steps{
                script{
                    echo "Deploying docker image.."
                }
            }
        }
    }
}