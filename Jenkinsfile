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
                terraform create--auto-approve
                aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
                '''
            }
        }
    }
}
