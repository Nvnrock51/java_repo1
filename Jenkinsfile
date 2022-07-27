pipeline{
    agent any
    tools {
        maven "Maven 3.6.3"
    }
    environment {
        NEXUS_VERSION = "nexus3.40.1-01"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "3.110.48.86:8081"
        NEXUS_REPOSITORY = "simple-app"
        NEXUS_CREDENTIAL_ID = "nexus3"
    }
    stages{
        stage("GIT checkout"){
            steps{
                checkout([$class: 'GitSCM',
                branches: [[name: '*/master']],
                extensions: [],
                userRemoteConfigs: [[url: 'https://github.com/Nvnrock51/java_repo1.git']
                ]
                ]
                )
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv target/*.war /var/lib/jenkins/workspace/simple-app/target/works-with-heroku"
            }
         }
         stage("Publish to Nexus Repository Manager") {
            steps {
         nexusArtifactUploader artifacts: 
         [
             [
                 artifactId: 'works-with-heroku',
                 classifier: '', 
                 file: '/var/lib/jenkins/workspace/simple-app/target/works-with-heroku', 
                 type: 'war'
                 ]
                 ],
                 credentialsId: 'nexus3',
                 groupId: 'works.buddy.samples',
                 nexusUrl: '3.110.48.86:8081',
                 nexusVersion: 'nexus3',
                 protocol: 'http',
                 repository: 'simpleapp-release',
                 version: '1.0.0'   
   }
}