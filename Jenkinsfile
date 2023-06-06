pipeline {
    agent any
    parameters {
        string(name: 'templateFileName', defaultValue: 'template.json', description: 'The template file name to deploy.')
        string(name: 'vnetName', defaultValue: 'vnet', description: 'The virtual network name to deploy.')
        string(name: 'resourceGroup', defaultValue: 'azure-load-balancer-introduction', description: 'The name for resource group to deploy template to.')
        string(name: 'vnetAddressPrefix', defaultValue: '10.0.0.0/12', description: 'Address space for Virtual Netwrok.')
        // choice(name: 'imageSku', choices: ['2022-Datacenter', '2021-Datacenter', '2020-Datacenter','2019-Datacenter'], description: 'The SKU of the image reference.')
        string(name: 'subnetName', defaultValue: 'clusterSubnet', description: 'The subnet name to deploy.')
        string(name: 'subnetAddressPrefix', defaultValue: '10.0.0.0/16', description: 'Address space for Subnet.')
    }
    stages {
        stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'gautam', url: 'https://github.com/gautam232019/IR-AzureTask.git'
            }
        }
        stage('Azure Login') {
                steps {
                    script {
                        withCredentials([usernamePassword(credentialsId: 'b4f7f50e-56a9-4c35-a1f1-34ac57881dc5',usernameVariable: 'fed6f9b4-34cf-4e76-b1fe-af331d0b194d' ,passwordVariable: 'Qh68Q~cavaMEN1X7PjF5c99CjZQNEPc52ka35deP')]) {
                            sh "az login --service-principal -u fed6f9b4-34cf-4e76-b1fe-af331d0b194d -p Qh68Q~cavaMEN1X7PjF5c99CjZQNEPc52ka35deP --tenant 2563c132-88f5-466f-bbb2-e83153b3c808"
                        }
                    }
                }
            }
        stage('Deploy ARM Template') {
                steps {
                    script {
                        sh "az deployment group create --resource-group ${params.resourceGroup} --template-file ${params.templateFileName} --parameters vnetName=${params.vnetName} vnetAddressPrefix=${params.vnetAddressPrefix} subnetName=${params.subnetName} subnetAddressPrefix=${params.subnetAddressPrefix}"
                    }
                }
            }
    }
}