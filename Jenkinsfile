pipeline{
    agent any

    tools{
        maven 'Maven'
    }

    environment {
        PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;${env.PATH}"
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-creds'
        DOCKERHUB_REPO = 'aleksi246/calc'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages{
        stage('build jar') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('build docker image') {
            steps{
                script{
                    docker.build("${DOCKERHUB_REPO}:${DOCKER_IMAGE_TAG}")
                }
            }
        }
        stage('push docker image'){
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS_ID){
                    docker.image("${DOCKERHUB_REPO}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}