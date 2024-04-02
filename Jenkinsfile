@Library('my-shared-library') _

pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/naman-6/devsecops-java-pipeline.git"
                )
            }
        }
        stage('Unit Test: maven') {
            steps {
                mvnTest()
            }
        }
    }
}