pipeline {
    agent any
    // parameters{
    //    string(name:'Branch_Name', defaultValue: 'main',description: 'Enter the branch name')
    // }
     environment{
    version= "1.3.0"
    }

    stages {
        stage('Hello') {
            steps {
                echo "${version}"
                echo 'Hello World  I dddam herenbjhbjddff454545'
            }
        }

        stage('testing') {
             when {
                 expression{

                     env.BRANCH_NAME == 'jan2024franklin'
            }

                }


            steps{
                echo 'Hello World'
            }

        }


        stage('Git Checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/jan2024franklin']], extensions: [], userRemoteConfigs: [[credentialsId: 'franklin-ibt', url: 'https://github.com/IBT-learning/ibt-maven.git']])
                sh 'ls -lrt'
               // sh 'echo $Branch_Name'

            }
        }

    }
    post {
        always {
          // Send email notification on success
          mail  to: 'recipient@example.com',
               subject: 'Build Successful',
               body: 'The build was successful!'
        }
      }
}

