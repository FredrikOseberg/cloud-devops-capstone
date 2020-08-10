pipeline {
    agent {
        dockerfile true
    }
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
                sh "docker push khare123/cloud-devops-capstone"
            }
        }
    }
}