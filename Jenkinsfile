pipeline {
    agent any

    environment {
        BUILD_DIR = 'build'
        DEPLOY_DIR = "${env.WORKSPACE}/deploy"
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
                    sh 'mkdir -p build'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the HTML Application...'
                script {
                    sh 'find . -maxdepth 1 ! -name build ! -name . -exec cp -r {} build/ \\;'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    sh '[ -f build/index.html ]'
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
            echo 'Build succeeded!'
        }
    }
}
