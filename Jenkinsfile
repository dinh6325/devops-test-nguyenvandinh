pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo '===== CHECKOUT SOURCE ====='
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '===== INSTALL DEPENDENCIES ====='
                echo 'HTML project - no external dependencies'
            }
        }

        stage('Build') {
            steps {
                echo '===== BUILD PROJECT ====='

                sh '''
                    if [ ! -f index.html ]; then
                        echo "ERROR: index.html not found!"
                        exit 1
                    fi

                    echo "index.html found"
                    echo "Build successful!"
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo '===== DEPLOY ====='
                echo 'Deploy step will be configured next'
            }
        }
    }

    post {
        success {
            echo '===== BUILD SUCCESS ====='
        }

        failure {
            echo '===== BUILD FAILED ====='
        }
    }
}