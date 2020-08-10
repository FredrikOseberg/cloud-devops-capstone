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
                def image = docker.build("khare123/cloud-devops-capstone")
                image.push()
            }
        }
    }
}