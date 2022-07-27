pipeline{
    agent any
    tools {
        maven "Maven 3.6.3"
    }
    environment {
        NEXUS_VERSION = "nexus3.40.1-01"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "3.110.48.86:8081"
        NEXUS_REPOSITORY = "simpleapp-release"
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
                 nexusUrl: 'http://13.233.96.18:8081/repository/simpleapp-release/',
                 nexusVersion: 'nexus3',
                 protocol: 'http',
                 repository: 'simpleapp-release',
                 version: '1.0.0'   
              }
          }
    }
    post {
        success {
	        mail bcc: '', body: 'Build configure check success', cc: '', from: '', replyTo: '', subject: 'Build Check', to: 'naveen.gaddam91@gmail.com'
        }
        failure {
    	    mail bcc: '', body: 'Build configure check fail', cc: '', from: '', replyTo: '', subject: 'Build Check', to: 'naveen.gaddam91@gmail.com'
	    }
	}
}
