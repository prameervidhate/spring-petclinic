pipeline {
    agent any

    environment {
        TOMCAT_USER = 'ec2-user'
        TOMCAT_IP = '54.198.144.124'
        TOMCAT_PATH = '/opt/tomcat/webapps'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/prameervidhate/spring-petclinic.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no target/*.war $ec2-user@$54.198.144.124:/opt/tomcat/webapps/petclinic.war
                ssh $$ec2-user@$54.198.144.124 "/opt/tomcat/bin/shutdown.sh"
                ssh $ec2-user@$54.198.144.124 "/opt/tomcat/bin/startup.sh"
                '''
            }
        }
    }
}
