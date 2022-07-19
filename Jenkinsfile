pipeline {
    agent {
       label 'tomcat-slave1'
}
    stages {
        stage('git checkout') {
            steps {
                echo 'this is git checkout stage'
                                   git 'https://github.com/sinshree/java_repo1.git'
            }
        }
        stage('build') {
            steps {
                 echo 'this is build stage'
                                    sh 'mvn clean install'
            }
        }
            
        stage('push to artifactory') {
            steps {
                echo 'this is the push stage'
            }
        }
        stage('deploy') {
            steps {
                 echo 'this is the deploy stage'
                                sh ' sudo cp /home/ec2-user/jenkins-slave1/workspace/tomcat-newjob1/target/*.war /opt/tomcat*/webapps/'
            }
        }
    }
}
