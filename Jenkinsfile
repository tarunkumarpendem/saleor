pipeline{
    agent any
    stages{
        stage('clone'){
            agent{
                 label 'node-1'
            }
            steps{
                git url: 'https://github.com/tarunkumarpendem/saleor.git',
                    branch: 'main'
            }
        }
        stage('docker_image_build and push'){
            agent{
                label 'node-1'
            }
            steps{
                sh 'docker image build -t saleor-core:dev1 .'
                sh 'docker image tag saleor-core:dev1 tarunkumarpendem/saleor-core:dev1'
                sh 'docker image push tarunkumarpendem/saleor-core:dev1'
            }
        }
        stage('eks_cluster'){
            agent{
                label 'eks-cluster'
            }
            steps{
                sh 'git clone https://github.com/hashicorp/learn-terraform-provision-eks-cluster'
                sh 'cd learn-terraform-provision-eks-cluster'
                sh 'terraform init && terraform apply -auto-approve'
                sh 'aws eks --region $(terraform output -raw region) update-kubeconfig \
                    --name $(terraform output -raw cluster_name)'
            }
        }
    } 
}