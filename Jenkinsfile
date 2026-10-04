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
                bat 'cd Backend\\todo-summary-assistant && mvnw.cmd clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'mysql-db-creds',
                        usernameVariable: 'SPRING_DATASOURCE_USERNAME',
                        passwordVariable: 'SPRING_DATASOURCE_PASSWORD'
                    ),
                    string(
                        credentialsId: 'cohere-api-key',
                        variable: 'COHERE_API_KEY'
                    )
                ]) {
                    bat '''
                        set SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/todo_db?createDatabaseIfNotExist=true
                        cd Backend\\todo-summary-assistant
                        mvnw.cmd test
                    '''
                }
            }
        }
    }
}