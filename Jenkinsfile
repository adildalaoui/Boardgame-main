pipeline {
    agent any
     
    tools {
        maven 'maven3.9'
        jdk 'jdk17'
    }

    stages {
        
        stage('Compile') {
            steps {
             sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
              sh 'mvn test' 
            }
        }
        
        stage('Build') {
            steps {
              sh "mvn package"
            }
        }
    }
post { 
    success {
        build job: 'job-2'
        }
    }
post { 
    success {
        build job: 'job-2'
    }

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
            <h3 style="color: white;">Pipeline Status: ${pipelineStatus.toUpperCase()}</h3>
            </div>
            <p>Check the <a href="${env.BUILD_URL}">console output</a>.</p>
            </div>
            </body>
            </html>
            """

            emailext (
                subject: "${jobName} - Build ${buildNumber} - ${pipelineStatus.toUpperCase()}",
                body: body,
                to: 'adil.dalaoui@yahoo.fr',
                from: 'adil.dalaoui@yahoo.fr',
                replyTo: 'adil.dalaoui@yahoo.fr',
                mimeType: 'text/html'
            )
        }
    }
}
}
