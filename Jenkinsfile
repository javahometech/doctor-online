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
            when {
                branch 'develop'
            }
            steps{
                 echo "Deploying to dev"
            }
        }
        stage("Tomcat Test Deploy"){
            when {
                branch 'test'
            }
            steps{
                echo "Deploying to test"
            }
        }
        stage("Tomcat Production Deploy"){
            when {
                branch 'main'
            }
            steps{
                 echo "Deploying to prod"
            }
        }
    }
    post {
      success {
        cleanWs()
      }
    }
}
