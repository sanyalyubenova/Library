pipeline {
    agent any

    tools {
        nodejs 'NodeJS-18'
    }

    stages {
        stage('Install dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Install Playwright browsers') {
            steps {
                bat 'npx playwright install --with-deps chromium'
            }
        }

        stage('Start server and run tests') {
            steps {
                bat '''
                    start /B npm start
                    npx wait-on http://localhost:3000 --timeout 60000
                    npm test
                '''
            }
        }
    }

    post {
        always {
            bat 'taskkill /F /IM node.exe'
        }
    }
}