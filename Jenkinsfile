pipeline {
    agent any
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/atharrvv/react-product-app.git'
            }
        }
        stage('Build images') {
            steps {
                script {
                    docker.build('eatherv/frontend', './frontend')
                    docker.build('eatherv/backend', './backend')
                    docker.build('eatherv/database', './database')
                }
            }
        }
        
        // stage('Docker hub') {
        //     steps {
        //         script {
        //             docker.withRegistry('https://index.docker.io/v1/', 'docker') {
        //                 docker.image("eatherv/frontend:latest").push()
        //                 docker.image("eatherv/backend:latest").push()
        //                 docker.image("eatherv/database:latest").push()
        //             }
        //         }
        //     }
        // }
        
        stage('Creating Container') {
            steps {
                script {
                    def dbCpntainer = docker
                        .image('eatherv/database')
                        .run('-d -p 3306:3306 --name database ')
                    
                    def backEnd = docker
                        .image('eatherv/backend')
                        .run('-d -p 8080:8080 --name backend')
                        
                    def frontEnd = docker
                        .image('eatherv/frontend')
                        .run('-d -p 3000:80 --name frontend')
                }
            }
        }
        // stage ('Image to DockerHub') {
        //     steps {
        //         script {
        //             withCredentials([usernamePassword(credentialsId: DOCKER_JENKINS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
        //                 sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
        //                 // Push the image
        //                 sh "docker push eatherv/frontend:latest"
        //             }
        //         }
        //     }
        // }
    }
}


