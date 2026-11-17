
pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out project from GitHub...'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Step: Checking web application files...'
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo 'Test Step: Validating project files...'
                bat '''
                    if not exist index.html exit /b 1
                    if not exist style.css exit /b 1
                    if not exist script.js exit /b 1
                    echo All required files are present.
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying web application...'
                bat '''
                    if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                    xcopy /Y /E index.html style.css script.js "%DEPLOY_DIR%\\"
                '''
            }
        }
    }stage('Deploy') {
    steps {
        echo 'Deploying web application...'
        bat '''
            if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
            copy /Y index.html "%DEPLOY_DIR%"
            copy /Y style.css "%DEPLOY_DIR%"
            copy /Y script.js "%DEPLOY_DIR%"
            echo Deployment completed successfully.
        '''
    }
}

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
            echo 'Visit: http://localhost/'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
