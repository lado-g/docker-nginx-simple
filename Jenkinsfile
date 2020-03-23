pipeline {
  
  
  agent agent { docker { image 'roffe/kubectl' } }


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
        stage ('k8s') {
          steps {
            withKubeConfig(clusterName: 'eks', contextName: '', credentialsId: 'eks', namespace: 'kube-system', serverUrl: 'https://B2EF2EDE4C3C11211A74ADFE80BA95C8.gr7.eu-central-1.eks.amazonaws.com') {
              withAWS(credentials: 'aws-credentials', region: 'eu-central-1'){
                    sh 'kubectl get pods' 
                }
              }
            }
        }   
        //stage('Building image') {
        //    steps{
        //      script {
        //        dockerImage = docker.build registry
        //      }
        //    }
        //  }
        //stage ('unit tests') {
//            steps {
//              script {
//                     sh '''
//                     python -m pytest --verbose --junit-xml test-reports/results.xml test_file.py
//                     '''
//              }
//            }
//        
//            post {
//                always {
//                    // Archive unit tests for the future
//                    junit 'test-reports/*.xml'
//                        
//                }
//            }
//        }
//
       //   stage('Push image') {
       //        steps {
       //            script {
       //          withDockerRegistry([url: registryurl ,credentialsId: "ecr:eu-central-1:ecr"]) {
       //              dockerImage.push(env.GIT_COMMIT)
       //              dockerImage.push("latest")
       //              dockerImage.push(env.DATE)
       //              
       //             }
       //         }
       //     }
       // }

            
    }

}
