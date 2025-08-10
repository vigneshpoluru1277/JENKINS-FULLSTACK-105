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

        stage('Copy Frontend Build to Backend') {
            steps {
                bat '''
                     rmdir /S /Q "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\reactstudentapi"
                     mkdir "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\reactstudentapi"
                     xcopy /E /I /Y dist\* "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\reactstudentapi"
                '''
            }
        }

        stage('Build Backend') {
            steps {
                dir('STUDENTAPI-SPRINGBOOT') {
                    bat 'mvn clean package'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                    del /Q "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\springbootstudentapi.war"
                    rmdir /S /Q "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\springbootstudentapi"
                    cd target
                    copy *.war "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\"
                    '''
            }
        }
    }

    post {
        success { echo 'Deployment Successful!' }
        failure { echo 'Pipeline Failed.' }
    }
}
