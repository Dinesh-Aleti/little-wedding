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
                docker build -t ${env.JOB_NAME}:latest .
//                 docker tag $env.JOB_NAME:latest $env.JOB_NAME:env.BUILD_NUMBER
                '''
            }
        }
    }
}
