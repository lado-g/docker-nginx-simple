pipeline {
  
  
  agent { docker { image 'roffe/kubectl' } }


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
            withKubeConfig(caCertificate: 'LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN5RENDQWJDZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJd01ETXhNVEUxTXpVek5sb1hEVE13TURNd09URTFNelV6Tmxvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTVgrCml4eWdNL2wvcE1iUTZ4OWJTNVBKWWc3cllCemhZTVl0dFVUN09JSENGc3hGcW5BVDJSY3lvUy9mZWljbXR1aVAKMkR1SjZtM09Xb0hZOW9IY21nVEhWRmVwT2c0bHJKSjFnZkRmTUJKYXd1Ui9mNU05N1B0dkt2VGlJU1ZsT0FMNQpuNkNpQlVQRURFVVZ1L2h1T2V2UW5IT2t3TVpSUHZKTDc2VTlLUG50RU1FS0FjSml0aFVRSkdNUnV2c2g3Zi9zCnR6L25rOGdEd0FteXBudkV0dTR6WDhRVG1DZFVmQWwvVGZuRXJzNXQ2S2FFZkVXc3VydFZpZUM1SnExQXlhNlAKaWlDVlI1NHdkMG1lWDhHK0RMUDBadkxodWVjeWZTRmE4dXkwWi9XUHJ2dlFWZ0p0aU8yQmZRVVZXOFRTUzhJdQoxQ2hBUjYrY2hrcFp6MXdreGNFQ0F3RUFBYU1qTUNFd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFKNUh2cEFncjBHUmIvQ3hXQ2VCdjEzQURKczkKZGVMTFIrWGZNN0JsSGF4aDNFY3dOY3hSU3dNZ3VmV0hGU2t5ZVlUeXJPVWMwcHY3SUFqUzIwYWdCYnFhT3M3Qwo4bkVXMXNieHoxZ2l4U1dQeVV0a2V5Ukk0eDYwVThvNURKV2thK2NOMjJBdkxOanJyMTVZVVdOSXVYVkNDblVjCitETUZrNHNhdkl6dkkydkZiQnB5dkV2cE9wVXdqdDhTOElFYnlvSVROUjJOc3dBeURXL0ZEWGp6UXI3L2pkbi8KdEJRckZkSmp0TC9EOTNwV2JJcCtxYjJLcjdJVXA0NGdIV2Y2VnJidEhaQ1loOWRPT3ZYcGVDazJNdUdacDBEQQpvZEJnck1FTlgyNGhhczBYWHk4ckp1aWhYTTd0aWYvYkVBVmdmYjBGUTZyQ1c2YTh3TjhsRDE0TG5OST0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=', clusterName: 'test', contextName: 'test', credentialsId: 'ecr:eu-central-1:ecr', namespace: 'test', serverUrl: 'https://B2EF2EDE4C3C11211A74ADFE80BA95C8.gr7.eu-central-1.eks.amazonaws.com') {
              sh 'kubectl get pods'
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
