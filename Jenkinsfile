pipeline{
    agent any
    environment {     
        JWT_SECRET = 'SDNCN23423TN394UFKND'
        MONGO_URL = 'mongodb+srv://charan03:030904@clusterecoverse.xxoya0d.mongodb.net/ecoverse'
        jwt_token = 'dhfmharnca394020'
    }
    stages{
        stage('Clone Git'){
            steps{
                git branch: 'main',
                url: 'https://github.com/chokshiyadav/SPE_MajorProject.git'
            }
        }
//         stage('Testing'){
//             steps{
//                 dir('api'){
//                     sh "npm install"
//                     sh "npm test"
//                 }
//             }
//         }
        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t frontend-image ./client'
            }
        }
         stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-image ./backend'
            }
        }
          stage('Push Images to DockerHub') {
            steps {

                 withCredentials([usernamePassword(credentialsId: 'DockerHubCred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                     sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                     sh 'docker tag frontend-image chokshi/frontend-image:latest'
                     sh 'docker push chokshi/frontend-image:latest'
                     sh 'docker tag backend-image chokshi/backend-image:latest'
                     sh 'docker push chokshi/backend-image:latest'
                }
            }
        }
//         stage('Ansible Deployment') {
//             steps {
//                 script {
//                     sh 'ansible-playbook -i inventory-k8 playbook-k8.yml'
//                 }
//             }
//         }
    }
}
