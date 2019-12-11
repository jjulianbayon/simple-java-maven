pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Checkout scm') {
            steps{
                checkout scm
            }
            
        }
        stage ('Build Release'){
            steps{
                sh 'mvn gitflow:release'
            }
        }
        /*stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }*/
        stage('Testeo') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Delivery') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
