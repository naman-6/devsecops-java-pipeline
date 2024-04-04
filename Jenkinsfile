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
        
    //     stage('Unit Test: Maven') {
    //         when { expression { params.action == 'create' } }
    //         steps {
    //             script {
    //                 mvnTest()
    //             }
    //         }
    //     }
        
    //     stage('Integration Test: Maven') {
    //         when { expression { params.action == 'create' } }
    //         steps {
    //             script {
    //                 mvnIntegrationTest()
    //             }
    //         }
    //     }
        

    //     stage('Static Code Analysis: SonarQube') {
    //         when { expression { params.action == 'create' } }
    //         steps {
    //             script {
    //                 def sonarCredentialsId = 'sonar-api'
    //                 staticCodeAnalysis(sonarCredentialsId)
    //             }
    //         }
    //     }
    }

    post {
        always {
            script {
                def jobName = env.JOB_NAME
                def buildNumber = env.BUILD_NUMBER
                def pipelineStatus = currentBuild.result ?: 'UNKNOWN'
                def bannerColor = pipelineStatus.toUpperCase() == 'SUCCESS' ? 'green' : 'red'
                def body = """
                    <html>
                        <body>
                            <div style="border: 4px solid ${bannerColor}; padding: 10px;">
                                <h2>${jobName} - Build ${buildNumber}</h2>
                                <div style="background-color: ${bannerColor}; padding: 10px;">
                                    <h3 style="color: white;">Pipeline Status:${pipelineStatus.toUpperCase()}</h3>
                                </div>
                                <p>Check the <a href="${BUILD_URL}">console output</a>.</p>
                            </div>
                        </body>
                    </html>"""
                
                emailtext (
                    subject: "${jobName} - Build ${buildNumber} - ${pipelineStatus.toUpperCase()}",
                    body: body,
                    to: 'naman.xy6@gmail.com',
                    from: 'jenkins@example.com',
                    replyTo: 'jenkins@example.com',
                    mimeType: 'text/html'
                )
            }
        }
    }
}