pipeline {
    agent any 

    stages {
        stage('Git Packer Template') { 
            steps { 
                sh 'rm -rvf bakery_django_base'
                sh 'git clone https://github.com/jakehigg/bakery_django_base.git' 
            }
        }
        stage('Bake') {
            steps {
                withCredentials([string(credentialsId: 'aws_access_key', variable: 'aws_access_key')]) {
                withCredentials([string(credentialsId: 'aws_secret_key', variable: 'aws_secret_key')]) {
                withCredentials([string(credentialsId: 'aws_account_id', variable: 'aws_account_id')]) {
                sh '''
                packer build -var "aws_access_key=$aws_access_key" -var "aws_secret_key=$aws_secret_key" -var "aws_account_id=$aws_account_id" -var "vpc_id=vpc-04bea57d" -var "subnet_id=subnet-86bb84aa" bakery_django_base/packer/bakery.json
                '''
                }}}
               
                }
            }
        }
    }

