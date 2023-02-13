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
    }
}
