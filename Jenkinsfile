pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token')
    }

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
                echo '===== DEPLOY TO VERCEL ====='

                sh '''
                    npx vercel --prod --token "$VERCEL_TOKEN" --yes --name devops-test-nguyenvandinh
                '''
            }
        }
    }

    post {
        success {
            echo '===== BUILD SUCCESS ====='
            echo '===== DEPLOY SUCCESS ====='
        }

        failure {
            echo '===== BUILD FAILED ====='
            echo '===== DEPLOY FAILED ====='
        }
    }
}