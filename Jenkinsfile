pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AKIAWMFUO72DMBGFMJZZ')   // Jenkins credentials ID
        AWS_SECRET_ACCESS_KEY = credentials('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')   // Jenkins credentials ID
        AWS_DEFAULT_REGION    = 'ap-south-1'   // apna AWS region
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/IamY0uu/Ansible.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                pip3 install boto3 botocore --user
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                ansible-playbook -i inventory launch-ec2.yml
                '''
            }
        }
    }

    post {
        success {
            echo ' EC2 Instance launched successfully via Ansible!'
        }
        failure {
            echo ' Something went wrong. Check logs.'
        }
    }
}
