@Library("jhc-libs") _

pipeline {
    agent any

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/javahometech/doctor-online'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Tomcat Dev Deploy"){
            steps{
                tomcatDeploy("172.31.30.174","ec2-user","tomcat-dev","doctor-online.war")
            }
        }
    }
    post {
      success {
        cleanWs()
      }
    }
}
