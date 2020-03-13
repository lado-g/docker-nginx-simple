pipeline {
  
  
  agent any


  environment {
    DATE  = sh(script: "echo `date +%Y-%m-%d-%H-%M-%S`", returnStdout: true).trim()
    registry = "558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world"
    dockerImage = ''
    registryurl=  "https://558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world"
    githuburl = 'https://github.com/lado-g/docker-nginx-simple.git'
  }
    parameters {
    gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
  }
  
  stages {
        
        stage('Example') {
          steps {
            git branch: "${params.BRANCH}", url: githuburl
          }
        }  
        stage('Building image') {
            steps{
              script {
                dockerImage = docker.build registry
              }
            }
          }

          stage('Push image') {
               steps {
                   script {
                 withDockerRegistry([url: registryurl ,credentialsId: "ecr:eu-central-1:ecr"]) {
                     dockerImage.push(env.GIT_COMMIT)
                     dockerImage.push("latest")
                     dockerImage.push(env.DATE)
                     
                    }
                }
            }
        }  
    }

}
