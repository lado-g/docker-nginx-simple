pipeline {
  agent {
    dockerfile {
      filename 'Dockerfile'
      args "-t 558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world:1.0"
    }

  }
  stages {
    stage('') {
      steps {
        echo 'hi'
      }
    }
    
    stage('Push image') {
         steps {
           withDockerRegistry([url: "https://558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world",credentialsId: "ecr:eu-central-1:ecr"]) {
           sh 'docker push 558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world:1.0'
               }
        }

  }
}
}
