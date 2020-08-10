pipeline {
    agent any
    registry = "khare123/cloud-devops-capstone"

    stages {
        stage('Lint') {
            steps {
                sh "tidy -q -e *.html"
            }
        }
        stage("Build image") {
            sh "docker build -t khare123/cloud-devops-capstone ."
        }
        stage("Push image") {
            sh "docker push khare123/cloud-devops-capstone"
        }
    }
}