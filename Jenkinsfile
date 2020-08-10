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
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {
                    sh '''
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        docker push khare123/cloud-devops-capstone
                    '''
                }
            }
        }
        stage("Set k8s context") {
            steps {
                withAWS(region:'eu-north-1', credentials: 'aws-static') {
                    sh '''
                        aws eks --region eu-north-1 update-kubeconfig --name prod
                        kubectl config use-context arn:aws:eks:eu-north-1:460355206366:cluster/prod
                    '''
                }
            }
        }
        stage("deploy image to k8s") {
            steps {
                withAWS(region:'eu-north-1', credentials: 'aws-static') {
                    sh '''
                        kubectl apply -f ./deployment.yaml
                    '''
                }
            }
        }
        stage("get url") {
            steps {
                withAWS(region:'eu-north-1', credentials: 'aws-static') {
                    sh '''
                        kubectl get services
                    '''
                }
            }
        }
    }
}