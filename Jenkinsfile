pipeline {
    agent any

    environment {
        APP_NAME = 'simple-html-app'
        BUILD_DIR = 'build'
        DEPLOY_DIR = '/var/www/html'  // Change this if deploying elsewhere
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out the code from GitHub...'
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                echo 'Setting up the environment...'
                script {
                    // Create a clean build directory
                    sh 'mkdir -p ${BUILD_DIR}'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the HTML Application...'
                script {
                    // Copy all files except the build directory itself
                    sh 'find . -maxdepth 1 ! -name build ! -name "." -exec cp -r {} ${BUILD_DIR} \\;'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    // Check if index.html exists in the build directory
                    sh 'if [ ! -f ${BUILD_DIR}/index.html ]; then echo "index.html not found!"; exit 1; fi'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the HTML Application...'
                script {
                    echo "Deploying to ${DEPLOY_DIR}"
                    sh 'cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/'
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Post-deployment steps, if any...'
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            deleteDir()
        }

        failure {
            echo 'Build failed!'
        }

        success {
            echo 'Build and deployment succeeded!'
        }
    }
}
