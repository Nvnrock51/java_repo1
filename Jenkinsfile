pipeline{
    agent any
    tools {
        maven "Maven 3.6.3"
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
                 nexusUrl: '3.108.219.11:8081',
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
