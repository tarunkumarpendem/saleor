pipeline{
    triggers{
        pollSCM('* * * * *')
    }
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
                sh """docker image build -t saleor-core:dev-1.0 .
                      docker image tag saleor-core:dev-1.0 tarunkumarpendem/saleor-core:dev-1.0
                      docker image push tarunkumarpendem/saleor-core:dev-1.0
                    """ 
            }
        }
    }
}