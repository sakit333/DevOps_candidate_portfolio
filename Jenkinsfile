pipeline {
    agent any

    environment {
        DEPLOY_PATH = '/var/www/html/'
    }

    stages {
        stage('Install httpd') {
            steps {
                script {
                    // Install httpd and start the service
                    sh "sudo yum install -y httpd"
                    sh "sudo systemctl start httpd"
                    sh "sudo systemctl enable httpd"
                }
            }
        }
        
        stage('Deploy Files') {
            steps {
                script {
                    // Deploy files to the specified path
                    sh "sudo cp -r * ${env.DEPLOY_PATH}"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
