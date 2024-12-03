pipeline {
    agent any
    stages {
        stage('Build images') {
            steps {
                script {
                    docker.build('eatherv/frontend', './frontend')
                    docker.build('eatherv/backend', './backend')
                }
            }
        }
        
        stage('Creating Container') {
            steps {
                script {

                    def frontEnd = docker
                        .image('eatherv/frontend')
                        .run('-d -p 3000:80 --name frontend')
                    
                    def backEnd = docker
                        .image('eatherv/backend')
                        .run('-d -p 8080:8080 --name backend')

                }
            }
        }

        stage('Docker hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'Docker') {
                        docker.image("eatherv/frontend:latest").push()
                        docker.image("eatherv/backend:latest").push()
                    }
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


