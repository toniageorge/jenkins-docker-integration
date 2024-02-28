pipeline{
    agent any
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
                    withCredentials([string(credentialsId: 'DockPwd', variable: 'dockPwd')]) {
                    bat 'docker login -u toniageorge -p ${dockPwd}'
                  }
                }
            }
        }
    }
}