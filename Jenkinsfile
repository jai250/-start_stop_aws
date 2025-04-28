pipeline {
    agent any

    environment {
        AWS_REGION = 'eu-north-1'          // change if needed
        INSTANCE_ID = 'i-04d58ddbb50fcc266'  // YOUR EC2 instance ID
    }

    stages {
        stage('Start EC2 Instance') {
            steps {
                echo 'Starting EC2 Instance...'
                sh '''
                    aws ec2 start-instances --instance-ids $INSTANCE_ID --region $AWS_REGION
                    aws ec2 wait instance-running --instance-ids $INSTANCE_ID --region $AWS_REGION
                '''
                echo 'EC2 instance is now running.'
            }
        }

        stage('Do Some Work') {
            steps {
                echo 'Simulating some work...'
                sh 'sleep 30' // sleep for 30 seconds
            }
        }

        stage('Stop EC2 Instance') {
            steps {
                echo 'Stopping EC2 Instance...'
                sh '''
                    aws ec2 stop-instances --instance-ids $INSTANCE_ID --region $AWS_REGION
                    aws ec2 wait instance-stopped --instance-ids $INSTANCE_ID --region $AWS_REGION
                '''
                echo 'EC2 instance is now stopped.'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
