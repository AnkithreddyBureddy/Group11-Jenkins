pipeline {
    agent any

    environment {
        BUILD_DIR = 'build'
        DEPLOY_DIR = '/var/www/html'
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
                    sh "mkdir -p ${BUILD_DIR}"
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the HTML Application...'
                script {
                    // Copy files except build dir itself
                    sh "find . -maxdepth 1 ! -name ${BUILD_DIR} ! -name . -exec cp -r {} ${BUILD_DIR}/ \\;"
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    sh "[ -f ${BUILD_DIR}/index.html ]"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the HTML Application...'
                script {
                    echo "Deploying to ${DEPLOY_DIR}"
                    sh """
                        mkdir -p ${DEPLOY_DIR}
                        cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/
                    """
                }
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
            echo 'Build and Deployment completed successfully!'
        }
    }
}
