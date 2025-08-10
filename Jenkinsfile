pipeline {
    agent any

    stages {
        
        stage('Build Frontend') {
            steps {
                dir('STUDENTAPI-REACT') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Clean Old Static Files in Backend') {
            steps {
                bat '''
                    rmdir /S /Q STUDENTAPI-SPRINGBOOT\\src\\main\\resources\\static
                    mkdir STUDENTAPI-SPRINGBOOT\\src\\main\\resources\\static
                '''
            }
        }

        stage('Copy Frontend Build to Backend') {
            steps {
                bat '''
                    xcopy /E /I /Y STUDENTAPI-REACT\\dist\\* STUDENTAPI-SPRINGBOOT\\src\\main\\resources\\static\\
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

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                    set "TOMCAT=C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1"
                    rmdir /S /Q "%TOMCAT%\\webapps\\myapp"
                    copy STUDENTAPI-SPRINGBOOT\\target\\*.war "%TOMCAT%\\webapps\\myapp.war"
                    '''
            }
        }
    }

    post {
        success { echo 'Deployment Successful!' }
        failure { echo 'Pipeline Failed.' }
    }
}
