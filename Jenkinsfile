pipeline {
    agent any
    stages {
        stage ('AZ login') {
            steps {
                script {
                    withCredentials([azureServicePrincipal('azure_principle')]) {
                        sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                        sh  'az acr login --name keanu'
                        }
                    }
                }
            }
        // stage('Build images') {
        //     steps {
        //         script {
        //             docker.build('keanu.azurecr.io/frontend-h', './frontend')
        //             docker.build('keanu.azurecr.io/backend-h', './backend')
        //         }
        //     }
        // }
        // stage('ACR Push') {
        //     steps {
        //         script {
        //             sh """
        //             docker push keanu.azurecr.io/frontend-h
        //             docker push keanu.azurecr.io/backend-h
        //             """
        //             }
        //         }
        //     }
        stage ('kubectl apply') {
            steps {
                script {
                    withCredentials([azureServicePrincipal('azure_principle')]){
                        sh 'az aks get-credentials --resource-group group --name rolex'
                        sh 'kubectl apply -f /home/chris/backend-h.yaml'
                        sh 'kubectl apply -f /home/chris/frontend-h.yaml'
                    }
                }
            }
        }
        // stage ('AKS') {
        //     steps {
        //         script{
        //             sh """
        //             az aks get-credentials --resource-group group --name rolex
        //             kubectl apply -f /home/chris/backend-h.yaml
        //             kubectl apply -f /home/chris/frontend-h.yaml
                    
        //             """
                    
        //         }
        //     }
        // }
        
    }
}

