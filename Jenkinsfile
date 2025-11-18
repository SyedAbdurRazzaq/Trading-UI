pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git 'https://github.com/betawins/Trading-UI.git'
            }
        }

        stage('Install npm prerequisites') {
            steps {
                // Enable legacy OpenSSL provider for Webpack builds
                withEnv(["NODE_OPTIONS=--openssl-legacy-provider"]) {
                    sh 'npm install'
                    sh 'CI=false npm run build'
                }

                // PM2 restart
                sh 'pm2 delete Trading-UI || true'
                sh 'pm2 --name Trading-UI start npm -- start'
            }
        }
    }
}

