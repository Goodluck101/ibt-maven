pipeline {
    agent any
    parameters {
      string(name:"Branch_Name", defaultValue: "master", description: "Enter branch to build")
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Vamsi') {
            steps {
                echo 'This is Vamsi'
            }
        }
        stage('Downloading Git Repo') {
             steps {
                 git branch: '$Branch_Name', changelog: false, credentialsId: 'GitHub_cred_vamsi', poll: false, url: 'https://github.com/VamsiKrishnaYadavLoya/demo-nov.git'
             }
        }
        stage('List Files') {
             steps {
                 bat 'dir'
             }
        }
    }
}
