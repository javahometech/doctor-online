@Library("jhc-libs") _

pipeline {
    agent any

    stages {
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
