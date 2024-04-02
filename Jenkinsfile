@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
        choice (name: 'action', choices: 'create\ndelete', description: 'Choose Create/Delete')
    }

    stages {
        stage('Git Checkout') {
            when { expression { params.action == 'create' } }
            steps {
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/naman-6/devsecops-java-pipeline.git"
                )
            }
        }
        
        stage('Unit Test: Maven') {
            when { expression { params.action == 'create' } }
            steps {
                script {
                    mvnTest()
                }
            }
        }
        
        stage('Integration Test: Maven') {
            when { expression { params.action == 'create' } }
            steps {
                script {
                    mvnIntegrationTest()
                }
            }
        }
        

        stage('Static Code Analysis: SonarQube') {
            when { expression { params.action == 'create' } }
            steps {
                script {
                    def sonarCredentialsId = 'sonar-api'
                    staticCodeAnalysis(sonarCredentialsId)
                }
            }
        }
    }
}