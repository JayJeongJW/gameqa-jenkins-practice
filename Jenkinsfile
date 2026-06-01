pipeline {
    agent any

    stages {
        stage('Check Node Version') {
            steps {
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'call npm install'
            }
        }

        stage('Install Newman Locally') {
            steps {
                bat 'call npm install --save-dev newman newman-reporter-htmlextra'
            }
        }

        stage('Start Mock Server') {
            steps {
                bat 'start "" /B node server.js'
                bat 'timeout /t 3 /nobreak'
            }
        }

        stage('Run Login API Test') {
            steps {
                bat 'if not exist newman mkdir newman'
                bat 'call npx newman run Login_API_Test.postman_collection.json -e GameQA_ENV.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export newman\\Login_Report.html --export-environment GameQA_ENV.postman_environment.json'
            }
        }

        stage('Run Ranking API Test') {
            steps {
                bat 'call npx newman run Ranking_API_Test.postman_collection.json -e GameQA_ENV.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export newman\\Ranking_Report.html'
            }
        }

        stage('Run Item Grant API Test') {
            steps {
                bat 'call npx newman run Item_Grant_API_Test.postman_collection.json -e GameQA_ENV.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export newman\\ItemGrant_Report.html'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'newman/*.html', allowEmptyArchive: true
        }
    }
}