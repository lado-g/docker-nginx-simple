pipeline {
  
  
  agent { docker { 
    image 'kubectl-with-aws-cli:1.0.3'
    args  '-v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock '
    }
  }


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
        
        stage('Git Branch') {
          steps {
            git branch: "${params.BRANCH}", url: githuburl
          }
        }  
        stage ('k8s-pods') {
          steps {
            withKubeConfig(clusterName: 'eks', contextName: '', credentialsId: 'eks', namespace: 'kube-system', serverUrl: 'https://F56D93F0BD9D9EFC60E3B17D008C1C51.gr7.eu-central-1.eks.amazonaws.com') {
              withAWS(credentials: 'lado', region: 'eu-central-1'){
                    sh 'kubectl get pods' 
                }
              }
            }
        }   
        stage('Building image') {
            steps{
              script {
                dockerImage = docker.build registry
              }
            }
          }
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
        stage ('k8s-update') {
          steps {
            withKubeConfig(clusterName: 'eks', contextName: '', credentialsId: 'eks', namespace: 'kube-system', serverUrl: 'https://F56D93F0BD9D9EFC60E3B17D008C1C51.gr7.eu-central-1.eks.amazonaws.com') {
              withAWS(credentials: 'lado', region: 'eu-central-1'){
                    sh 'kubectl set image  deployment/hello-world hello-world=gcr.io/google-samples/node-hello:1.0 --namespace default' 
                }
              }
            }
        }   

            
    }

}
