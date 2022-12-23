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
                sh 'docker image build -t saleor-core:dev .'
                sh 'docker image tag saleor:dev tarunkumarpendem/saleor-core:dev'
                sh 'docker image push tarunkumarpendem/saleor-core:dev'
            }
        }
        stage('eks_cluster'){
            agent{
                label 'eks-cluster'
            }
            steps{
                git url: 'https://github.com/hashicorp/learn-terraform-provision-eks-cluster'
            }
        }
        stage('cluster-node_configure'){
            agent{
                label 'eks-cluster'
            }
            steps{
                sh 'terraform init && terraform apply -auto-approve'
                sh 'aws eks --region $(terraform output -raw region) update-kubeconfig \
                    --name $(terraform output -raw cluster_name)'
            }
        }
    } 
}