pipeline {
    agent any

    environment {
        BUILD_DIR = 'build'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                echo 'Setting up the environment...'
                // Create a build directory
                sh 'mkdir -p $BUILD_DIR'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the HTML application...'
                // Copy the necessary files to the build directory
                sh 'cp index.html README.md $BUILD_DIR'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // You can add your test steps here
                // For example, if you have unit tests, you can run them in this stage.
                // Since this is a simple HTML app, you may skip this stage or add a simple check like validating the HTML.
                sh 'echo "No tests for HTML app"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Assuming you have a simple deploy step like moving the files to a web server or another location
                // For example, you can use `scp` to copy the files to a remote server.
                sh 'cp -r $BUILD_DIR/* /var/www/html'  // This is just an example, adapt to your own deployment needs.
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Cleaning up workspace...'
                cleanWs()  // Clean the workspace after the build is done
            }
        }
    }

    post {
        always {
            echo 'Build finished'
        }

        success {
            echo 'The build was successful!'
        }

        failure {
            echo 'The build failed.'
        }
    }
}
