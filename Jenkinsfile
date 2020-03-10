pipeline {
  
  
  agent any


  environment {
    registry = "558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world"
    dockerImage = ''
  }

  stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
    stage('Push image') {
         steps {
           withDockerRegistry([url: "https://558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world",credentialsId: "ecr:eu-central-1:ecr"]) {
               dockerImage.push()
            }
        }
    }
}

