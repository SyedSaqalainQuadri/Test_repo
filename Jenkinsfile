pipeline {
    agent any

    environment {
        REMOTE_USER = "ubuntu"                 // Remote Jenkins server username
        REMOTE_HOST = "172.31.11.241"       // Remote Jenkins server IP/Hostname
        REMOTE_DIR = "/home/ubuntu/scp" // Directory on the remote Jenkins server
        LOCAL_ZIP_FILE = "C:/Users/user/Downloads/testfolder.zip"         // Name of the ZIP file to transfer
    }

    stages {
        stage('Upload ZIP File to Remote Jenkins') {
            steps {
                script {
                    sh """
                        scp -i C:/Users/user/Downloads/uzair-devops.pem ${LOCAL_ZIP_FILE} ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}
                    """
                    echo "File transferred successfully to remote Jenkins server!"
                }
            }
        }

        stage('Verify Transfer on Remote Jenkins') {
            steps {
                script {
                    sh """
                        ssh -i  C:/Users/user/Downloads/uzair-devops.pem ${REMOTE_USER}@${REMOTE_HOST} "ls -l ${REMOTE_DIR}/${LOCAL_ZIP_FILE}"
                    """
                    echo "Verification complete!"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed! Check logs for errors."
        }
    }
}


