pipeline{
    agent any

    stages {
    stage('Git checkout') {
                steps {
                    checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/feature_nnamdi']], extensions: [], userRemoteConfigs: [[credentialsId: 'ibt', url: 'https://github.com/IBT-learning/ibt-maven.git']]]
                }
            }
     stage('Validate')
     {
        steps{
            withMaven(maven: 'maven_3.8') {
                sh "mvn validate"
            }
        }
     }
     stage('Compile')
          {
             steps{
                 withMaven(maven: 'maven_3.8') {
                   sh "mvn compile"
                 }
             }
          }
     stage('Run tests')
          {
             steps{
                 withMaven(maven: 'maven_3.8') {
                                 sh "mvn test"
                 }
             }
          }
      stage('SonarQube Analysis') {
       environment{
            scannerHome = tool 'ibt-sonarqube';
       }
           steps{
           withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
             sh "$scannerHome/bin/sonar-scanner"
           }
          }
         }
       stage('Package')
            {
               steps{
                   withMaven(maven: 'maven_3.8') {
                         sh "mvn package"
                  }
               }
            }
       stage('Upload to Artifactory')
       {
            steps{
                withCredentials([file(credentialsId: 'mvn_settings_gunjan', variable: 'settings')]) {
                withMaven(maven: 'maven_3.8') {
                    sh "mvn deploy -s $settings"
                   }
                }
            }
       }
       stage('upload Artifactory - configFile')
       {
            steps{
                configFileProvider([configFile(fileId: 'jfrog-mvn-settings', targetLocation: 'mvn_settings', variable: 'mvn_settings')]) {
                withMaven(maven: 'maven_3.8') {
                   sh "mvn deploy -s $mvn_settings"
                  }
                }
            }
       }
       stage('Vulnerability scan - Dependency Check')
       {
            steps{
                     dependencyCheck additionalArguments: '''
                                                           -o "./"
                                                           -s "./"
                                                           -f "ALL"
                                                           --prettyPrint ''', odcInstallation: 'dependency-check'
                       dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
       }
       stage('Configure Dev Server')
       {
            steps{
                ansiblePlaybook(
                become: true,
                colorized: true,
                credentialsId: 'vm-ssh',
                disableHostKeyChecking: true,
                inventory: 'hosts',
                playbook: 'tomcat.yaml'
                )
            }
       }
       stage('Deploy to Dev server')
       {
        steps{
            script{
                def remote = [name: 'IBT-dev', host: '165.22.224.106', allowAnyHosts: true]
                withCredentials([usernamePassword(credentialsId: 'for-IBT-dev01Server', passwordVariable: 'password', usernameVariable: 'username')]) {
                    remote.password = password
                    remote.user = username
                    sshPut remote: remote, from: 'target/ibt-maven-1.0.0.jar' , into: '/opt/tomcat/webapps'
                }

            }
        }
       }
    }
}
