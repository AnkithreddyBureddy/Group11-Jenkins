pipeline {
    agent any

    environment {
        APP_NAME = 'simple-html-app'
        BUILD_DIR = 'build'
        DEPLOY_DIR = '/var/www/html'  // Modify this if deploying to a different directory
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
                    // Create a build directory to hold the files for deployment
                    sh 'mkdir -p ${BUILD_DIR}'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the HTML Application...'
                script {
                    // Since it's a static HTML app, we simply copy the files to the build directory
                    sh 'cp -r * ${BUILD_DIR}'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    // Check if the essential files exist in the build directory
                    sh 'if [ ! -f ${BUILD_DIR}/index.html ]; then echo "index.html not found!"; exit 1; fi'
                    sh 'echo "index.html found, continuing with the build!"'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the HTML Application...'
                script {
                    // Ensure the deploy directory exists, create it if necessary
                    sh 'mkdir -p ${DEPLOY_DIR}'
                    // Deploy the HTML files to the server directory
                    sh 'cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/'
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Cleaning up workspace...'
                // Optional cleanup after deployment (e.g., removing temporary files)
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            deleteDir() // Clean up the workspace after the build is finished
        }

        success {
            echo 'Build succeeded!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
