pipeline {
    agent any

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
             steps {
                 echo 'Hello World, This is a testing Jenkinsfile'
             }
        }
        stage('Git checkout') {
             steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub-login-creds', url: 'https://github.com/Goodluck101/ibt-maven.git']])
                sh 'ls -ltr'
             }
             }
    }
}
