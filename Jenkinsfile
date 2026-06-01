pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Check Node Tool') {
            steps {
                bat 'echo Jenkins bat works'
                bat 'cd'
                bat 'where node'
                bat 'node -v'
                bat 'where npm'
                bat 'npm -v'
                bat 'where npx'
                bat 'npx -v'
            }
        }
    }
}
