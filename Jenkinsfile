pipeline {
    agent any
    // environment {
    //     AZURE_CLIENT_ID = credentials('AZURE_CLIENT_ID')
    //     AZURE_CLIENT_SECRET = credentials('AZURE_CLIENT_SECRET')
    //     AZURE_TENANT_ID = credentials('AZURE_TENANT_ID')
    // }
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/atharrvv/react-product-app.git'
            }
        }
        stage ('azure login') {
            steps {
                script {
                    sh '''
                    az login --service-principal \
                        --username "bf8b3f40-649a-4ba6-9564-f24c3841c6ca" \
                        --password "iRK8Q~fkLX7k8ewTTh7q~Zkf3pV_qiA4MncQoc-L" \
                        --tenant "d3f47893-5a40-4c35-8758-698ada11b86e"
                    echo "Successfully logged in to Azure."
                    az account show
                    '''
                }
            }
        }
        // stage('vault') {
        //     steps {
        //         script {
        //             sh 'export MYSQL_ROOT_PASSWORD=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-ROOT-PASSWORD" --query "value" -o tsv)'
        //             sh 'export MYSQL_USER=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-USER" --query "value" -o tsv)'
        //             sh 'export MYSQL_PASSWORD=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-PASSWORD" -o tsv)'
        //             sh 'export MYSQL_DATABASE=$(az keyvault secret show --vault-name "dhanush" --name "MYSQL-DATABASE" -o tsv)'
        //         }
        //     }
        // }
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
        // 
        // stage('Cleanup') {
        //     steps {
        //         cleanWs()  // This removes files and workspace after the job
        //     }
        // }
    }
}

