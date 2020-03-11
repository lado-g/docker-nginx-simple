pipeline {
  
  
  agent any


  environment {
    registry = "558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world"
    dockerImage = ''
  }
    parameters {
    gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
  }
  
  stages {
        
        stage('Example') {
          steps {
            git branch: "${params.BRANCH}", url: 'https://github.com/lado-g/docker-nginx-simple.git'
          }
        }  
        stage('Building image') {
            steps{
              script {
                dockerImage = docker.build registry + ":$GIT_COMMIT"
              }
            }
          }

          stage('Push image') {
               steps {
                   script {
                 withDockerRegistry([url: "https://558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world",credentialsId: "ecr:eu-central-1:ecr"]) {
                     dockerImage.push()
                     
                    }
                }
            }
        }  
    }

}
