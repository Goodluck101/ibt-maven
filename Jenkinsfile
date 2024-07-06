pipeline {
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
            }
        }
        stage('test') {
            steps {
                echo 'Hello World, This is a test'
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
    }
}
