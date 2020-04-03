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
        stage ('ECR login') {
            steps {
              script{
                def login = ecrLogin()  
                sh login
                
              }
              }
        }

          stage('Push image') {
               steps {
                   script {
                 //withDockerRegistry([url: registryurl ]) {
                 //    dockerImage.push(env.GIT_COMMIT)
                 //    dockerImage.push("latest")
                 //    dockerImage.push(env.DATE)
                     //docker tag dockerImage 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:latest
                     //docker tag dockerImage 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:prod
                     docker push dockerImage 
                     //docker push 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:latest
                     //docker push 139339523421.dkr.ecr.us-east-1.amazonaws.com/ecr-upload-test:prod
                     
                    //}
                }
            }
        
        }    
    }

}
