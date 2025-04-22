pipeline {
    agent any

    environment {
        TOMCAT_USER = 'ec2-user'
        TOMCAT_IP = 'your-tomcat-ec2-public-ip'
        TOMCAT_PATH = '/opt/tomcat/webapps'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
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
                scp -o StrictHostKeyChecking=no target/*.war ${TOMCAT_USER}@${TOMCAT_IP}:${TOMCAT_PATH}/petclinic.war
                ssh ${TOMCAT_USER}@${TOMCAT_IP} "/opt/tomcat/bin/shutdown.sh"
                ssh ${TOMCAT_USER}@${TOMCAT_IP} "/opt/tomcat/bin/startup.sh"
                '''
            }
        }
    }
}
