pipeline {
    agent any

    environment {
        APP_NAME = 'simple-html-app'
        BUILD_DIR = 'build'
        DEPLOY_DIR = '/var/www/html'  // You can change this depending on where you want to deploy
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                echo 'Setting up the environment...'
                script {
                    // No environment setup is needed for basic HTML app
                    // Just creating a build directory for structure
                    sh 'mkdir -p ${BUILD_DIR}'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the HTML Application...'
                script {
                    // In this case, there is no real "build" step, since it's a static HTML app.
                    // We will simply copy the HTML files to the build directory.
                    sh 'cp -r * ${BUILD_DIR}'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    // In this case, we don't have any specific tests for a static HTML app,
                    // but you could add steps to check for file existence or structure here.
                    // For example:
                    sh 'if [ ! -f ${BUILD_DIR}/index.html ]; then echo "index.html not found!"; exit 1; fi'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the HTML Application...'
                script {
                    // For deployment, we'll assume you're deploying to a directory on a server.
                    // You can replace this with your actual deployment logic (e.g., using FTP, SSH, etc.)
                    echo "Deploying to ${DEPLOY_DIR}"
                    sh 'cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/'
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Cleaning up...'
                // Cleanup steps, if needed
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            deleteDir() // Clean up the workspace after the build is finished
        }
    }
}
