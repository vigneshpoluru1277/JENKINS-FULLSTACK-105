pipeline {
    agent any

    stages {
        // ===== FRONTEND =====
        stage('Delete Old Frontend Deployment') {
            steps {
                bat '''
                    rmdir /S /Q "C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps/reactstudentapi"
                '''
            }
        }

        stage('Build Frontend') {
            steps {
                dir('STUDENTAPI-REACT') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                bat '''
                    mkdir "C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps/reactstudentapi"
                    xcopy /E /I /Y STUDENTAPI-REACT/dist/* "C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps/reactstudentapi"
                '''
            }
        }

        // ===== BACKEND =====
        stage('Delete Old Backend Deployment') {
            steps {
                bat '''
                    del /Q "C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps/springbootstudentapi.war"
                    rmdir /S /Q "C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps/springbootstudentapi"
                '''
            }
        }

        stage('Build Backend') {
            steps {
                dir('STUDENTAPI-SPRINGBOOT') {
                    bat 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                bat '''
                    copy STUDENTAPI-SPRINGBOOT/target/*.war "C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps/springbootstudentapi.war"
                '''
            }
        }
    }

    post {
        success { echo 'Deployment Successful!' }
        failure { echo 'Pipeline Failed.' }
    }
}
