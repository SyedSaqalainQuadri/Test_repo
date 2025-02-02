pipeline {
    agent any

    environment {
        SOURCE_PATH = 'C:/Users/user/Downloads/testfolder.zip'
        DESTINATION_PATH = '/home/ec2-user/zip'
        REMOTE_USER = 'ec2-user' 
        REMOTE_HOST = '172.31.14.176'
        SSH_KEY = 'C:/Users/user/Downloads/uzair-devops.pem' // Replace with actual key path
    }

    stages {
        stage('Verify SSH Access') {
            steps {
                script {
                    echo 'Checking SSH access...'
                    sh "ssh -i ${env.SSH_KEY} -o StrictHostKeyChecking=no ${env.REMOTE_USER}@${env.REMOTE_HOST} 'echo SSH Connection Successful'"
                }
            }
        }

        stage('Transfer to Remote Server') {
            steps {
                script {
                    echo 'Ensuring destination directory exists on remote server...'
                    sh "ssh -i ${env.SSH_KEY} -o StrictHostKeyChecking=no ${env.REMOTE_USER}@${env.REMOTE_HOST} 'mkdir -p ${env.DESTINATION_PATH}'"

                    echo 'Transferring ZIP file to remote server...'
                    sh "scp -i ${env.SSH_KEY} -o StrictHostKeyChecking=no '${env.SOURCE_PATH}' ${env.REMOTE_USER}@${env.REMOTE_HOST}:${env.DESTINATION_PATH}/"
                }
            }
        }
    }

    post {
        success {
            echo 'File copy successful'
        }
        failure {
            echo 'File copy failed'
        }
    }
}
