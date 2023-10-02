pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install > build-log.txt 2>&1'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                sh 'mvn test > test-log.txt 2>&1'
            }
        }
        
        stage('Code Analysis') {
            steps {
                sh 'mvn sonar:sonar > code-analysis-log.txt 2>&1'
            }
        }
        
        stage('Security Scan') {
            steps {
                sh 'dependency-check.sh --project "My Project" --scan . > security-scan-log.txt 2>&1'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                sh './deploy-staging.sh > deploy-staging-log.txt 2>&1'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                sh './run-integration-tests.sh > integration-tests-staging-log.txt 2>&1'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                sh './deploy-production.sh > deploy-production-log.txt 2>&1'
            }
        }
    }

    post {
        always {
            script {
                // Concatenate all log files into one
                sh 'cat build-log.txt test-log.txt code-analysis-log.txt security-scan-log.txt deploy-staging-log.txt integration-tests-staging-log.txt deploy-production-log.txt > all-logs.txt'
                // Get the content of all-logs.txt
                def logContent = readFile 'all-logs.txt'
                mail (
                    subject: "Pipeline Completion: ${currentBuild.fullDisplayName}",
                    body: "The pipeline has completed. See details: ${env.BUILD_URL}\n\nLogs:\n${logContent}",
                    to: 'ahmadeiraj@gmail.com'
                )
            }
        }
    }
}
