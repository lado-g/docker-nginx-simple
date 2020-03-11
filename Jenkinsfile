pipeline {
  
  
  agent any


  environment {
    registry = "558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world"
    dockerImage = ''
    GITHUB_PROJECT="https://github.com/lado-g/docker-nginx-simple.git"
    GITHUB_CREDENTIALS_ID="github"
  }
  stages {
        stage ("Listing Branches") {
            steps {
                echo "Initializing workflow"
                //checkout code
                echo GITHUB_PROJECT
                git url: GITHUB_PROJECT, credentialsId: GITHUB_CREDENTIALS_ID
                sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' >branches.txt'
                sh 'cut -d '/' -f 2 branches.txt > branch.txt'
                //sh "sed s'/origin"\'///g branches.txt > branch.tx"
                //sed 's/$/from S0 to S1/'
            }
        }
        stage('get build branch Parameter User Input') {
            steps {
                liste = readFile 'branch.txt'
                echo "please click on the link here to chose the branch to build"
                env.BRANCH_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!',
                parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
            }
        }

        stage('Checkout external proj') {
            steps {
                echo "${env.BRANCH_SCOPE}"
                git branch: "${env.BRANCH_SCOPE}",
                credentialsId: 'Telcel',
                url: 'https://github.com/lado-g/docker-nginx-simple.git'

                sh "ls -lat"
            }
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
                   script {
                 withDockerRegistry([url: "https://558860702682.dkr.ecr.eu-central-1.amazonaws.com/hello-world",credentialsId: "ecr:eu-central-1:ecr"]) {
                     dockerImage.push()

                    }
                }
            }
        }

    }

}

