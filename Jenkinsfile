@Library("jhc-libs") _

pipeline {
    agent any

    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Upload Artifacts"){
            steps{
               script{
                    def pom = readMavenPom file: 'pom.xml'
                    def version = pom.version
                    def repoName = version.endsWith("SNAPSHOT") ? "do-snapshot": "do-release"
                    nexusArtifactUploader artifacts: [[artifactId: 'doctor-online', classifier: '', file: 'target/doctor-online.war', type: 'war']], 
                        credentialsId: 'nexus3', 
                        groupId: 'in.javahome', 
                        nexusUrl: '172.31.47.53:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: repoName, 
                        version: version
               }
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
