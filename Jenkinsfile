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
            )
        ]) {
            bat '''
                echo MySQL username: %SPRING_DATASOURCE_USERNAME%
                if "%SPRING_DATASOURCE_PASSWORD%"=="" (
                    echo MySQL password variable is EMPTY
                    exit /b 1
                ) else (
                    echo MySQL password variable is SET
                )

                cd Backend\\todo-summary-assistant
                mvnw.cmd test
            '''
        }
    }
}
}
}