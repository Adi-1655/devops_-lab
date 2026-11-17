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
                echo 'Test Step: Validating HTML file...'
                bat 'tidy -errors -q index.html'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying web application...'
                bat 'xcopy /Y /E index.html style.css script.js "%DEPLOY_DIR%\\"'
            }
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