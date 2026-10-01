pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token')
        TELEGRAM_TOKEN = credentials('telegram-bot-token')
        TELEGRAM_CHAT_ID = credentials('telegram-chat-id')
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
                    curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" \
                        -d chat_id="${TELEGRAM_CHAT_ID}" \
                        --data-urlencode "text=🚀 DEPLOY STARTED
Project: devops-test
Branch: main"

                    npx vercel --prod --token "$VERCEL_TOKEN" --yes --name devops-test-nguyenvandinh
                '''
            }
        }
    }

    post {
        success {
            echo '===== BUILD SUCCESS ====='
            echo '===== DEPLOY SUCCESS ====='

            sh '''
                curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" \
                    -d chat_id="${TELEGRAM_CHAT_ID}" \
                    --data-urlencode "text=✅ DEPLOY SUCCESS
Project: devops-test
Branch: main
URL: https://devops-test-nguyenvandinh.vercel.app"
            '''
        }

        failure {
            echo '===== BUILD FAILED ====='
            echo '===== DEPLOY FAILED ====='

            sh '''
                curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" \
                    -d chat_id="${TELEGRAM_CHAT_ID}" \
                    --data-urlencode "text=❌ DEPLOY FAILED
Project: devops-test
Branch: main
Please check Jenkins."
            '''
        }
    }
}