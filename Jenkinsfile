pipeline {
    agent any
    stages {
        stage('terraform') {
            steps {
                sh '''
                terraform destroy
                '''
            }
        }
    }
}