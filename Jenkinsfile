pipeline {
    agent any

    stages {
        stage('Delete Old Frontend Deployment') {
            steps {
                bat '''
                if exist "C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1\\webapps\\reactstudentapi" (
                    rmdir /S /Q "C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1\\webapps\\reactstudentapi"
                ) else (
                    echo "No old frontend deployment found, skipping delete."
                )
                '''
            }
        }

        stage('Build Frontend') {
            steps {
                bat 'echo Building frontend...'
                // Add your actual frontend build commands here
            }
        }

        stage('Deploy Frontend') {
            steps {
                bat 'echo Deploying frontend...'
                // Add your actual deployment steps here
            }
        }

        stage('Delete Old Backend Deployment') {
            steps {
                bat '''
                if exist "C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1\\webapps\\backendapi" (
                    rmdir /S /Q "C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1\\webapps\\backendapi"
                ) else (
                    echo "No old backend deployment found, skipping delete."
                )
                '''
            }
        }

        stage('Build Backend') {
            steps {
                bat 'echo Building backend...'
                // Add your backend build commands here
            }
        }

        stage('Deploy Backend') {
            steps {
                bat 'echo Deploying backend...'
                // Add your backend deployment steps here
            }
        }
    }
}
