pipeline{
    agent any
    environment {
        KUBECONFIG = credentials('K8sconfig')
        DOCKPWD =  credentials('Docker_password_jenkins')
    }
    tools{
        maven 'maven-3.9.6'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/toniageorge/jenkins-docker-integration']])
                bat 'mvn clean install'
            }
        }
        stage('Build a docker image'){
            steps{
                script{
                    bat 'docker build -t toniageorge/docker-jenkins-integration .'
                }
            }
        }
        stage('deploy docker image to docker hub'){
            steps{
                script{
                    bat 'docker login -u toniageorge -p {}'

                }
            }
        }
        stage('deploy to kubectl'){
            steps{
                script{
                    bat "kubectl apply --kubeconfig=${KUBECONFIG} -f deploymentservice.yaml"
                }
            }
        }
    }
}