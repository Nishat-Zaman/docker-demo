pipeline {
    agent any
    environment {
    imagename = "nishatzaman/docker-jenkins"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  stages {
    stage('Cloning Git') {
        steps {
            git([url: 'https://github.com/Nishat-Zaman/docker-demo.git', branch: 'master'])
        }
        }
        stage('Building image') {
        steps{
            script {
            dockerImage = docker.build imagename
            }
        }
        }
        stage('Deploy Image') {
        steps{
            script {
            docker.withRegistry( '', registryCredential ) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
            }
            }
        }
        }
        stage('Remove Unused docker image') {
        steps{
            sh "docker rmi $imagename:$BUILD_NUMBER"
            sh "docker rmi $imagename:latest"
        }
        }
  }
  
}
