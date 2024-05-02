pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/MuhsinBinen/demoJenkinsDocker']]
                )
                bat 'mvn clean install'
            }
        }

        stage('Build docker image'){
            steps{
                script{
                    docker.build("deneme1:${env.BUILD_NUMBER}")
                }
            }
        }



        stage('Push image to Hub'){
            steps{
                script{
                    docker.image("deneme1:${env.BUILD_NUMBER}").run("-d -p 8082:8082 --name demo-container")
                }
            }
        }
    }

}