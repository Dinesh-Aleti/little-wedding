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
                rsync -a /var/lib/jenkins/workspace/fashion_project/ root@52.91.125.168:/var/www/html/
            }
        }
    }
}
