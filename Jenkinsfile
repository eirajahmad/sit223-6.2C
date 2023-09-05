pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                // Use Maven to build the project
                sh 'mvn clean install'
            }
        }
        
        stage('Unit & Integration Tests') {
            steps {
                // Run tests with Maven
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                // Integrate with SonarQube (assuming you've set it up)
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                // Use OWASP Dependency-Check (you'll need to set this up)
                sh 'dependency-check.sh --project MyProject --scan ./path'
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Deploy to AWS EC2 (this will vary based on your setup)
                sh './deploy-to-staging.sh'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Run tests on staging
                sh './run-integration-tests.sh'
            }
        }

        stage('Deploy to Production') {
            steps {
                // Deploy to AWS EC2
                sh './deploy-to-production.sh'
            }
        }
    }

    post {
        failure {
            // Send email on failure
            mail to: 'ahmadeiraj@gmail.com', subject: 'Pipeline Failed', body: 'Logs attached.', attachLog: true
        }
    }
}
