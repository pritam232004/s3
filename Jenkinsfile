pipeline {
    agent any

    environment {
        BUCKET_NAME = 'www.aboutpritam.live'
        SOURCE_DIR = '.'  // or "." if in root
    }

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/pritam232004/s3.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                echo "Deploying to S3..."
                aws s3 sync $SOURCE_DIR s3://$BUCKET_NAME --delete
                echo "Deployment complete."
                '''
            }
        }
    }
}
