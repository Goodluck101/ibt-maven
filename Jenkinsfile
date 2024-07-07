pipeline {
environment {
    version = '1.3.0'
    }
    tools {
            maven 'Maven_3.9'
        }
    agent any
    parameters {
    string (name: 'Branch_Name', defaultValue: 'main', description: 'Enter branch to checkout')
           choice(name: 'CHOICES', choices: ['one', 'two', 'three'], description: 'Choose a number')
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Hello2') {
            steps {
                echo 'Hello World, This is stage 2'
                echo '${env.version}'
            }
        }
        stage('test') {
        environment {
                    version2 = '1.5.0'
                    }
            steps {
                echo 'Hello World, This is a test'
                echo "${env.version2}"
                echo '${env.version2}'
            }
        }
        stage('testing Jenkinsfile') {
        when {
           expression {
             env.Branch_Name=='feature-gunjvm'
             }
        }
             steps {
                 echo 'Hello World, This is a testing Jenkinsfile'
             }
        }
        stage('Git checkout') {
             steps {
                checkout scmGit(branches: [[name: '*/$Branch_Name']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub-login-creds', url: 'https://github.com/Goodluck101/ibt-maven.git']])
                sh 'ls -ltr'
                sh 'echo $Branch_Name $CHOICES'
             }
        }
        stage('testing webhooks') {
             steps {
                echo 'Hello World!!, This is a test for webhook modified'
             }
        }
/*        post {
        always {
        emailext body: '''Dear Team,

        Your build job has been completed.
        Kindly review the status.

        Best regards,
        NexGenix DevOps Team.''', subject: 'Post Email Test', to: 'ekeomaadiole@gmail.com'
        }
        } */

    }
}
