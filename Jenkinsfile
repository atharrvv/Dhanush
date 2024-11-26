pipeline {
    agent any
        environment {
        MYSQL_ROOT_PASSWORD = sh(script: 'az keyvault secret show --vault-name "dhanush" --name "MYSQL-ROOT-PASSWORD" --query "value" -o tsv', returnStdout: true).trim()
        MYSQL_USER = sh(script: 'az keyvault secret show --vault-name "dhanush" --name "MYSQL-USER" --query "value" -o tsv', returnStdout: true).trim()
        MYSQL_PASSWORD = sh(script: 'az keyvault secret show --vault-name "dhanush" --name "MYSQL-PASSWORD" -o tsv', returnStdout: true).trim()
        MYSQL_DATABASE = sh(script: 'az keyvault secret show --vault-name "dhanush" --name "MYSQL-DATABASE" -o tsv', returnStdout: true).trim()
    }
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/atharrvv/react-product-app.git'
            }
        }
        stage('Azure login') {
            steps {
                withCredentials([azureServicePrincipal('AZURE_PRICIPLE')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                    sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
                    sh 'az resource list'
                }
            }
        }
        stage('trial') {
            steps {
                script {
                    echo "MYSQL_ROOT_PASSWORD: ${env.MYSQL_ROOT_PASSWORD}"
                    echo "MYSQL_USER: ${env.MYSQL_USER}"
                    echo "MYSQL_PASSWORD: ${env.MYSQL_PASSWORD}"
                    echo "MYSQL_DATABASE: ${env.MYSQL_DATABASE}"
                }
            }
        }
        // stage('Build images') {
        //     steps {
        //         script {
        //             // docker.build('eatherv/frontend', './frontend')
        //             // docker.build('eatherv/backend', './backend')
        //             // docker.build('eatherv/database', './database')
        //         }
        //     }
        // }
        
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
        //                 .run('-d -p 3306:3306 --name database -e MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD} -e MYSQL_USER=${MYSQL_USER} -e MYSQL_PASSWORD=${MYSQL_PASSWORD} -e MYSQL_DATABASE=${MYSQL_DATABASE}')
                    
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
    }
}


