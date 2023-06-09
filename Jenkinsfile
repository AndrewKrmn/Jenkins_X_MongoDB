pipeline {
    agent any
    
    stages {
        stage('create docker image mongodb') {
            steps {
                sh '''
                docker build -t chikibevchik/mongo:mongodb .
                docker push chikibevchik/mongo:mongodb
                '''
            }
        }
        stage('Create docker network') {
            steps {
                sh '''
                docker network create mongo-net
                '''
            }
        }
        stage('run mongo database') {
            steps {
                sh '''
                docker run -d --name mongo-container --network mongo-net -p 27017:27017 chikibevchik/mongo:mongodb

                '''
            }
        }
        stage('run mongo express') {
            steps {
                sh '''
                docker run -d --name mongo-express-container --network mongo-net -p 8081:8081 -e ME_CONFIG_MONGODB_SERVER=mongo-container -e ME_CONFIG_BASICAUTH_USERNAME=admin -e ME_CONFIG_BASICAUTH_PASSWORD=password chikibevchik/mongo:mongo-express

                '''
            }
        }
    }
}
