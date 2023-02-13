pipeline {
    agent any

    stages {
        stage ('git checkout') {
            steps {
                git 'https://github.com/Dinesh-Aleti/little-wedding.git'
            }
        }
        stage ('copy source code') {
            steps {
                sh 'rsync -a /var/lib/jenkins/workspace/fashion_project/ root@172.31.54.166:/var/www/html/'
            }
        }
        stage ('build image') {
            agent {
            label 'prod-server'
            }
            steps {
                sh '''
                cd /var/www/html/
                docker build -t $JOB_NAME:v1 .
                docker tag $JOB_NAME:v1 $JOB_NAME:latest
                docker stop $JOB_NAME
                docker run -dit -p 8082:80 --name $JOB_NAME -v /var/www/html/:/var/www/html --rm $JOB_NAME:v1
                '''
            }
        }
    }
}
