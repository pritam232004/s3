pipeline {
    agent any

    environment {
        BUCKET_NAME = 'www.aboutpritam.live' 
        SOURCE_DIR = 'web'                  
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Check AWS CLI') {
            steps {
                sh '''
                if ! command -v aws &> /dev/null
                then
                    echo "❌ AWS CLI is not installed."
                    exit 1
                fi
                aws --version
                '''
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                echo "Uploading $SOURCE_DIR to s3://$BUCKET_NAME ..."
                aws s3 sync $SOURCE_DIR s3://$BUCKET_NAME --delete
                echo "✅ Deployment to S3 completed."
                '''
            }
        }
    }
}
