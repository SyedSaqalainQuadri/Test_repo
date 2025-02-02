pipeline {
    agent any

    environment {
        SOURCE_PATH = 'C:/Users/user/Downloads/testfolder.zip'  // Source directory on the local system
        DESTINATION_PATH = '/home/ec2-user/zip' // Destination directory on target server
        REMOTE_SERVER = 'ec2-user@172.31.14.176' // Corrected by removing the trailing space
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
                    echo 'Transferring ZIP file to remote server using rsync...'
                    sh "rsync -avz -e 'ssh -o StrictHostKeyChecking=no' ${SOURCE_PATH} ${REMOTE_SERVER}:${DESTINATION_PATH}/"
                }
            }
        }
    }

        post {
            success {
                    echo 'file copy successful'
                }
            failure {
                    echo 'file copy failed'
            }
        }
}
