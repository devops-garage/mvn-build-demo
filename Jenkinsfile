pipeline {
    agent any

    tools {
        maven 'maven3'   // must match the name in Tools config
        jdk 'jdk25'      // must match the JDK name
    }

    stages {
        stage('Verify Tools') {
            steps {
                sh 'mvn -version'
                sh 'java -version'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/devops-garage/mvn-build-demo.git', credentialsId: 'devops-garage'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

    }
}
