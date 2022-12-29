pipeline {
    agent {
        label 'node'
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('terraform') {
            steps {
                sh '''
                terraform init
                terraform destroy --auto-approve
                aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
                '''
            }
        }
        stage ('kubectl apply') {
            steps {
                sh '''
                kubectl apply -f spring.yml
                kubectl get all
                '''
            }
        }
    }
}