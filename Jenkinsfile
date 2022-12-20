pipeline{
    agent{
        label 'test'
    }
    stages{
        stage('clone'){
            steps{
                git url: 'https://github.com/tarunkumarpendem/saleor.git',
                    branch: 'main'
            }
        }
        stage('docker_image_build'){
            steps{
                sh 'docker image build -t saleor-core:dev .'
                sh 'docker image tag saleor:dev tarunkumarpendem/saleor-core:dev'
                sh 'docker image push tarunkumarpendem/saleor-core:dev'
            }
        }
    } 
}