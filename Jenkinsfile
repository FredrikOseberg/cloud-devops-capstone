pipeline {
    agent any
    stages {
        stage('Lint') {
            steps {
                sh "tidy -q -e *.html"
            }
        }
        stage("Build image") {
            steps {
                sh "sudo docker build -t khare123/cloud-devops-capstone ."
            }
        }
        stage("Push image") {
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {
                    sh "sudo docker push khare123/cloud-devops-capstone"
                }
            }
        }
    }
}