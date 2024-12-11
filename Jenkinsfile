pipeline {
    agent any
    stages {
        stage('AZ login') {
            steps {
                script {
                    // Hardcoded Service Principal credentials
                    def appId = 'bf8b3f40-649a-4ba6-9564-f24c3841c6ca'
                    def password = 'iRK8Q~fkLX7k8ewTTh7q~Zkf3pV_qiA4MncQoc-L'
                    def tenantId = 'd3f47893-5a40-4c35-8758-698ada11b86e'
                    // Azure login using Service Principal
                    sh """
                    az login --service-principal \
                    -u ${appId} \
                    -p ${password} \
                    --tenant ${tenantId}
                    az acr login --name keanu
                    """
                }
            }
        }
        stage('Build images') {
            steps {
                script {
                    docker.build('keanu.azurecr.io/frontend-h', './frontend')
                    docker.build('keanu.azurecr.io/backend-h', './backend')
                }
            }
        }
        stage('ACR Push') {
            steps {
                script {
                    sh """
                    docker push keanu.azurecr.io/frontend-h
                    docker push keanu.azurecr.io/backend-h
                    """
                    }
                }
            }
        stage ('AKS') {
            steps {
                script{
                    sh """
                    az aks get-credentials --resource-group group --name rolex
                    kubectl apply -f /home/chris/backend-h.yaml
                    kubectl apply -f /home/chris/frontend-h.yaml
                    
                    """
                    
                }
            }
        }
        
    }
}

