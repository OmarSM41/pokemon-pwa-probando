pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('VERCEL_TOKEN')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/OmarSM41/pokemon-pwa-probando.git'
            }
        }

        stage('Install Node') {
            steps {
                bat '''
                    echo Instalando Node 18...
                    curl -o node.msi https://nodejs.org/dist/v18.19.0/node-v18.19.0-x64.msi
                    msiexec /i node.msi /quiet /norestart
                '''
            }
        }

        stage('Verify Node') {
            steps {
                bat '''
                    node -v
                    npm -v
                '''
            }
        }

        stage('Install dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build PWA') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                bat '''
                    npm install -g vercel
                    vercel deploy --prod --token %VERCEL_TOKEN% --yes
                '''
            }
        }
    }
}

