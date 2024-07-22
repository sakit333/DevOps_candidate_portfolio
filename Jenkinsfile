pipeline {
    agent any

    environment {
        DEPLOY_PATH = '/var/www/html/'
    }

    stages {
        stage('install httpd')  {
            steps {
                script {
                    sh "sudo yum install httpd -y"
                    sh "sudo systemctl start httpd"
                }
            }
        }
        stage('Deploy Files') {
            steps {
                script {
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
