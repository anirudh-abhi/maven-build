pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('GitHub Stage') {
            steps {
                git branch: 'main', credentialsId: 'anirudh', url: 'https://github.com/anirudh-abhi/maven-build.git'
            }
        }
        stage('Maven Build Stage') {
            environment {
                MVN_HOME = tool name: 'Maven', type: 'maven'
            }
            steps {
                script {
                    sh "${MVN_HOME}/bin/mvn clean package"
                }
            }
        }
        stage('Deploy Stage') {
            steps {
                script {
                    // Ensure webapps directory exists
                    sh 'sudo mkdir -p /usr/local/tomcat/apache-tomcat-9.0.91/webapps'
                    
                    // Copy .war file to Tomcat webapps directory
                    sh 'sudo cp target/02-maven-webapp.war /usr/local/tomcat/apache-tomcat-9.0.91/webapps'
                }
            }
        }
    }
}
