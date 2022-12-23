pipeline {
    agent any
    stages {
        stage('terraform') {
            steps {
                sh '''
                 terraform init
                 terraform apply --auto-approve
                '''
            }
        }
    }
}