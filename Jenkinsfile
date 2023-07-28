pipeline {
    agent any

    environment {
        dockerimagename = "sathish143kumar/nodeapp"
        dockerImage = ""
        gitCredentials = 'gitrepo' // Replace with the ID of the Git credentials you added in Jenkins
    }
    
    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', credentialsId:'gitrepo', url: 'https://github.com/sathis14hkumar/taskjenkins.git'
    
        }
    }
    stage('build'){
          steps{
            echo 'build done'
          }
          }

stage('Push Notification') {
    steps {
        script {
            withCredentials([string(credentialsId: 'TELEGRAM_TOKEN', variable: 'TOKEN'),
                             string(credentialsId: 'CHAT_ID', variable: 'CHAT_ID')]) {
                def buildStatus = currentBuild.result ?: 'UNKNOWN'
                def consoleOutput = ""

                // Capture console output
                try {
                    consoleOutput = sh(returnStdout: true, script: 'echo "Build started" && ./your_build_script.sh')
                } catch (e) {
                    consoleOutput = "Error occurred during build:\n${e}"
                    buildStatus = 'FAILED'
                }

                def message = "<b>Project</b>: POC\n" +
                              "<b>Branch</b>: master\n" +
                              "<b>Build</b>: ${buildStatus}\n" +
                              "<b>Console Output</b>:\n${consoleOutput}"

                sh """
                    curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode="HTML" -d text="${message}"
                """
            }
        }
    }
}


          }
          }
