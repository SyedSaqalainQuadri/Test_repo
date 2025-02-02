pipeline {
    agent any

    environment {
        SOURCE_PATH = 'C:/Users/user/Downloads/testfolder.zip'  // Windows path (ensure it exists)
        DESTINATION_PATH = '/home/ec2-user/zip' 
        REMOTE_SERVER = 'ec2-user@172.31.14.176'
    }

    stages{
        stage('Transfer to Remote Server') {
            steps {
                script {
                    echo 'Transferring ZIP file to remote server using SCP...'
                    sh "scp '${env.SOURCE_PATH}' ${env.REMOTE_SERVER}:${env.DESTINATION_PATH}/"
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

