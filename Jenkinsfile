pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'cd Backend\\todo-summary-assistant && mvnw.cmd clean package'
            }
        }
       stage('Test') {
           steps {
               bat 'cd Backend\\todo-summary-assistant && mvnw.cmd test'
           }
       }

    }
}