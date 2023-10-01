pipeline {
    agent any 

    stages {
        stage('Stage 1 - Build') {
            steps {
                echo 'Building the project...'
                // Add your build steps here
            }
        }
        stage('Stage 2 - Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                // Add your test steps here
            }
        }
        stage('Stage 3 - Code Analysis') {
            steps {
                echo 'Analyzing code...'
                // Add your code analysis steps here
            }
        }
        stage('Stage 4 - Security Scan') {
            steps {
                echo 'Scanning for security vulnerabilities...'
                // Add your security scan steps here
            }
        }
        stage('Stage 5 - Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Add your deployment to staging steps here
            }
        }
        stage('Stage 6 - Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Add your integration tests on staging steps here
            }
        }
        stage('Stage 7 - Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Add your deployment to production steps here
            }
        }
    }
    
    post {
        always {
            echo 'Sending notification email...'
            // Configure and send your notification email here
        }
        success {
        emailext (
            subject: "Jenkins Pipeline Success: ${currentBuild.fullDisplayName}",
            body: "The pipeline has completed successfully. See details: ${env.BUILD_URL}",
            to: 'ahmadeiraj@gmail.com'
        )
    }
    }
}
