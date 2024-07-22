pipeline {
    agent any

    environment {
        DEPLOY_PATH = '/var/www/html/'
    }

    stages {
        stage('Check and Install httpd') {
            steps {
                script {
                    // Check if httpd is installed
                    def httpdInstalled = sh(script: 'rpm -q httpd', returnStatus: true) == 0

                    if (httpdInstalled) {
                        echo 'httpd is already installed.'
                    } else {
                        echo 'httpd is not installed. Installing now...'
                        sh "sudo yum install -y httpd"
                    }

                    // Ensure httpd service is started and enabled
                    sh "sudo systemctl start httpd || true"
                    sh "sudo systemctl enable httpd || true"
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
