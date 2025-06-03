pipeline {
    agent any

    tools {
        nodejs 'Node' // Only NodeJS goes here
    }

    environment {
        // Add this only if your SonarQube setup needs authentication
        // SONAR_TOKEN = credentials('sonar-token-id') 
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
                sh 'npm test || true'
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    // 'MySonarQube' should match the name of the SonarQube server defined under:
                    // Manage Jenkins → Configure System → SonarQube servers
                    withSonarQubeEnv('MySonarQube') {
                        sh 'sonar-scanner'
                    }
                }
            }
        }
    }
}
