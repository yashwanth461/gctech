pipeline {
    agent { label 'slave' }
    
    tools {
        maven 'maven'
    }

    stages {
        stage('Checkout Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/yashwanth461/gctech.git'
            }
        }
        
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t yaeshvann/gtech ."
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'yashid') {
                        sh 'docker push yaeshvann/gtech:latest'
                    }
                }
            }
        }

        stage('Kubernetes Deploy') {
            steps {
                script {
                    sh '''
                    kubectl config use-context minikube
                    kubectl apply -f deploy.yml --validate=false
                    '''
                }
            }
        }
    }
}

