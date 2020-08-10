pipeline {
    environment {
        imageName = "khare123/cloud-devops-capstone"
        registryCredential = "docker"
        image = ''
    }
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
                script {
                    image = docker.build(imageName)
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    image.push()
                }
            }
        }
    }
}