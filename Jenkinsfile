pipeline {
  
  
  agent any


  environment {
    DATE  = sh(script: "echo `date +%Y-%m-%d-%H-%M-%S`", returnStdout: true).trim()
    registry = "280259655306.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test"
    dockerImage = ''
    registryurl=  "https://280259655306.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test"
    githuburl = 'https://github.com/lado-g/docker-nginx-simple.git'
  }
    
  stages {
        
        stage('Building image') {
            steps{
              script {
                dockerImage = docker.build registry
              }
            }
          }
        //stage ('unit tests') {
        //    steps {
        //      script {
        //             sh '''
        //             python -m pytest --verbose --junit-xml test-reports/results.xml test_file.py
        //             '''
        //      }
        //    }
        //
        //    post {
        //        always {
        //            // Archive unit tests for the future
        //            junit 'test-reports/*.xml'
        //                
        //        }
        //    }
        //}

          stage('Push image') {
               steps {
                   script {
                 withDockerRegistry([url: registryurl ,credentialsId: "ecr:us-east-1:aws-staging"]) {
                     dockerImage.push(env.GIT_COMMIT)
                     dockerImage.push("latest")
                     dockerImage.push(env.DATE)
                     
                    }
                }
            }
        
        }    
    }

}
