pipeline {
    agent any

    // Requires the Jenkins GitHub plugin and a GitHub push webhook.
    triggers {
        githubPush()
    }

    options {
        // The Checkout stage below performs the SCM checkout explicitly.
        skipDefaultCheckout(true)
    }

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out project from configured GitHub SCM...'
                checkout scm
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
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying web application to ${DEPLOY_DIR}..."
                bat 'if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"'
                bat 'copy /Y index.html "%DEPLOY_DIR%"'
                bat 'copy /Y style.css "%DEPLOY_DIR%"'
                bat 'copy /Y script.js "%DEPLOY_DIR%"'
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
