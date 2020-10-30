pipeline {
  environment {
    imagename = "my-flask-image:latest"
    registryCredential = 'julian-dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/julianNinoo/Devops.git', branch: 'master', credentialsId: 'git'])

      }
    }
    stage('Building image') {
      steps{
        script {
	  sh 'cd /home/juliannino00/Devops/practicaFlaskJenkins'
	  sh 'docker build -t my-flask-image:latest .'
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
