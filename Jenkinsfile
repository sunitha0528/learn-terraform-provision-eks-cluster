pipeline {
    agent any
    stages {
        stage('terraform') {
            steps {
                sh '''
                terraform init
                terraform apply --auto-approve
                aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
                curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
                chmod +x ./kubectl
                kubectl cluster-info
                kubectl get no
                kubectl apply -f saleor
                '''
            }
        }
    }
}