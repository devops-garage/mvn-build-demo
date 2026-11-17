pipeline {
    agent { label 'jenkins-agent-slave' }
    tools {
        maven 'maven3'
        jdk 'jdk25'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                sh 'mvn validate'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Clean Package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Install') {
            steps {
                sh 'mvn install'
            }
        }
    }

    post {
        success {
            echo 'All Maven stages passed'
        }
        failure {
            echo 'Build failed, check the console output'
        }
    }
}
