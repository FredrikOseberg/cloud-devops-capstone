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
                sh "docker build -t khare123/cloud-devops-capstone ."
            }
        }
        stage("Push image") {
            steps {
                withCredentials('dockerhub') {
                    sh "docker push khare123/cloud-devops-capstone"
                }
            }
        }
    }
}