pipeline {
    agent {
        docker {
            image 'maven:3.9.2'
            args '-v /root/.m2:/root/.m2'
        }
    }
     environment {
        MAVEN_OPTS = '-Dmaven.repo.local=$WORKSPACE/.m2/repository'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
