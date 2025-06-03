pipeline {
    agent any
    tools {
        nodejs 'Node'
        sonarQubeScanner 'SonarQube Scanner for Jenkins Pipeline' 
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/trungquantrannguyen/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true' // Allows pipeline to continue despite test failures
            }
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                sh 'sonar-scanner -Dsonar.login=${SONAR_TOKEN}'
            }
        }
    }
}
