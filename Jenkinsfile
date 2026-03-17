pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        S3_BUCKET = 'static-website-project-krishna'
        DISTRIBUTION_ID = 'YOUR_CLOUDFRONT_ID'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync . s3://$S3_BUCKET --delete
                '''
            }
        }

        stage('Invalidate CloudFront') {
            steps {
                sh '''
                aws cloudfront create-invalidation \
                --distribution-id $DISTRIBUTION_ID \
                --paths "/*"
                '''
            }
        }
    }
}
