//this is the code for deployment
pipeline {
    agent any
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'master', url: 'https://github.com/chandrasekharpb/javaparser-maven-sample.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deploy') {
            steps {
			
                sshagent(['my-aws-creds']) {
                  sh'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipelinebuild-deploy/target/javaparser-maven-sample-1.0-SNAPSHOT.jar ec2-user@172.31.3.236:/opt/apache-tomcat-9.0.54/webapps/'
                }
            }
        }
    }
}
