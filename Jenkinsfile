pipeline {
  
  
  agent any


  environment {
    DATE  = sh(script: "echo `date +%Y-%m-%d-%H-%M-%S`", returnStdout: true).trim()
    registry = "139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test"
    dockerImage = ''
    registryurl=  "https://139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test"
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
                     withAWS(role:'jenkins-execution-role', roleAccount:'917656499435')
                     def login = ecrLogin()  
                     sh login
                     sh 'docker push 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:latest'
                     //docker push 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:latest
                     //docker push 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:prod
                     
                    //}
                }
            }
        
        }    
    }

}
