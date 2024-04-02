pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/naman-6/devsecops-java-pipeline.git'
                }
            }
        }
    }
}