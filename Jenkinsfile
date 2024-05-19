pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/vijay3639/sunday-project.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t mynewimage /var/lib/jenkins/workspace/kops-project'
                sh 'sudo docker tag mynewimage vijay3639/mynewimage:latest'
                sh 'sudo docker tag mynewimage vijay3639/mynewimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push vijay3639/mynewimage:latest'
                sh 'sudo docker image push vijay3639/mynewimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/kops-project/pod.yml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
