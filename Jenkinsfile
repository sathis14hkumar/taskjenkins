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
            def buildStatus = currentBuild.result ?: 'UNKNOWN'
            def messageText

            if (buildStatus == 'SUCCESS') {
                messageText = "<b>Project</b> : Jenkinspvt \\n" +
                              "<b>Branch</b>: main \\n" +
                              "<b>Build</b>: OK \\n" +
                              "<b>Test suite</b> = TEST CASE PASSED"
            } else {
                messageText = "<b>Project</b> : Jenkinspvt \\n" +
                              "<b>Branch</b>: main \\n" +
                              "<b>Build</b>: ERROR \\n" +
                              "<b>Test suite</b> = TEST CASE FAILED"
            }

            withCredentials([
                string(credentialsId: 'TELEGRAM_TOKEN', variable: 'TOKEN'),
                string(credentialsId: 'CHAT_ID', variable: 'CHAT_ID')
            ]) {
                sh """
                    curl -s -X POST "https://api.telegram.org/bot${TOKEN}/sendMessage" \
                    -d "chat_id=${CHAT_ID}" \
                    -d "parse_mode=HTML" \
                    -d "text=${messageText}"
                """
            }
        }
    }
}

          }
          }
