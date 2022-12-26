pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('terraform') {
            steps {
                sh '''
                terraform init
                terraform apply --auto-approve
                aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)

                '''
            }
        }
        stage ('kubectl apply') {
            steps {
                sh '''
                kubectl cluster-info
                kubectl apply -f saleor.yml
                kubectl apply -f cache.yml
                kubectl apply -f db-service.yml
                kubectl get po
                '''
            }
        }
    }
}