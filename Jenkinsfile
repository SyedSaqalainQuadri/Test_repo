pipeline {
    agent any

    environment {
        SOURCE_PATH = 'C:/Users/user/Downloads/testfolder.zip'  // Windows path
        DESTINATION_PATH = '/home/ec2-user/zip' 
        REMOTE_SERVER = 'ec2-user@172.31.14.176'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'Fetching source files...'
                }
            }
        }

        stage('Transfer to Remote Server') {
            steps {
                script {
                    echo 'Ensuring destination directory exists on remote server...'
                    sh "ssh -o StrictHostKeyChecking=no ${env.REMOTE_SERVER} 'mkdir -p ${env.DESTINATION_PATH}'"

                    echo 'Transferring ZIP file to remote server using SCP...'
                    sh "scp -o StrictHostKeyChecking=no '${env.SOURCE_PATH}' ${env.REMOTE_SERVER}:${env.DESTINATION_PATH}/"
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
