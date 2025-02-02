pipeline {
    agent any

    environment {
        SOURCE_PATH = 'C:/Users/user/Downloads/testfolder.zip'  // Windows path (ensure it exists)
        DESTINATION_PATH = '/home/ubuntu/scp' 
        REMOTE_SERVER = 'ubuntu@172.31.11.241'
    }

    stages{
        stage('Transfer to Remote Server') {
            steps {
                script {
                    echo 'Transferring ZIP file to remote server using SCP...'
                    sh "scp -o StrictHostKeyChecking=no -i /c/Users/user/Downloads/uzair-devops.pem /c/Users/user/Downloads/testfolder.zip ubuntu@172.31.11.241:/home/ubuntu/scp/"
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

