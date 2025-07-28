pipeline {
    agent any

    tools {
        maven 'maven3.9.9'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/DevOpsPracticewithKKFunda/Mavenwebapplication.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }

        stage('Deploy To Nexus') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('Deploy App To Tomcat') {
            steps {
                sh '''
                curl -u naga:Password --upload-file /var/lib/jenkins/workspace/DeclarativePL/target/maven-web-application.war \
                "http://35.179.173.8:8080/manager/text/deploy?path=/maven-web-application&update=true"
                '''
            }
        }
    }
}
