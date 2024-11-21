pipeline {
    agent any
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/atharrvv/react-product-app.git'
            }
        }
        stage('vault') {
            steps {
                script {
                    sh export MYSQL_ROOT_PASSWORD=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-ROOT-PASSWORD" --query "value" -o tsv)
                    sh export MYSQL_USER=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-USER" --query "value" -o tsv)
                    sh export MYSQL_PASSWORD=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-PASSWORD" -o tsv)
                    sh export MYSQL_DATABASE=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-DATABASE" -o tsv)
                }
            }
        }
        stage('Build images') {
            steps {
                script {
                    // docker.build('eatherv/frontend', './frontend')
                    // docker.build('eatherv/backend', './backend')
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
        
        // stage('Creating Container') {
        //     steps {
        //         script {
        //             def dbCpntainer = docker
        //                 .image('eatherv/database')
        //                 .run('-d -p 3306:3306 --name database')
                    
        //             def backEnd = docker
        //                 .image('eatherv/backend')
        //                 .run('-d -p 8080:8080 --name backend')
                        
        //             def frontEnd = docker
        //                 .image('eatherv/frontend')
        //                 .run('-d -p 3000:80 --name frontend')
        //         }
        //     }
        // }
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
        // 
        // stage('Cleanup') {
        //     steps {
        //         cleanWs()  // This removes files and workspace after the job
        //     }
        // }
    }
}

