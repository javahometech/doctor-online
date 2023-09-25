pipeline{
    agent any
    stages{

        stage("Maven Build"){
            steps{
               sh "mvn clean package" 
            }
        }
        stage("Dev Deploy"){
            steps{
                sshagent(['tomcat-dev']) {
                    // COPY WAR FILE TO TOMCAT
                    sh "scp -o StrictHostKeyChecking=no target/doctor-online.war ec2-user@172.31.13.20:/opt/tomcat9/webapps"
                    // Stop tomcat
                    sh "ssh ec2-user@172.31.13.20 /opt/tomcat9/bin/shutdown.sh"
                    // start tomcat
                    sh "ssh ec2-user@172.31.13.20 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
