pipeline {
    agent any
//     environment {
//         withDockerRegistry(credentialsId: 'jenkins-dockerhub-login') {
//         }
//     }

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
                docker build -t $JOB_NAME:$BUILD_NUMBER .
                docker tag $JOB_NAME:$BUILD_NUMBER dineshaleti/$JOB_NAME
                '''
            }
        }
        stage ('pushing to dockerhub') {
            agent {
            label 'prod-server'
            }
            steps {
                script {
                    withDockerRegistry(credentialsId: 'jenkins-dockerhub-login') {
                            // some block
                    }
                sh '''
                cd /var/www/html/
                docker push dineshaleti/$JOB_NAME:latest
                '''
                }
            } 
        }
        
    }
}
