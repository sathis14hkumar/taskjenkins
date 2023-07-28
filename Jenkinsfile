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
                git branch: 'main', credentialsId:'gitrepo', url: 'https://github.comsathis14hkumar/taskjenkins.git'
    
        }

        // Add more stages for building, testing, deploying, etc.
        // ...
        } 
    }
    post {
        success {
            echo "Pipeline Passed!"
            sendTelegramNotification("Pipeline Passed!")
        }
       failure {
            script {
                echo "Pipeline Failed!"
                def failedStages = []
                def failedMessages = []
                for (stage in currentBuild.rawBuild.getExecution().getCurrentStage().getStages()) {
                    if (stage.getHasFailure()) {
                        failedStages.add(stage.getName())
                        failedMessages.add(stage.getError().toString())
                    }
                }
                def errorMessage = "Pipeline Failed in the following stages:\n"
                for (int i = 0; i < failedStages.size(); i++) {
                    errorMessage += "${failedStages[i]}: ${failedMessages[i]}\n"
                }
                sendTelegramNotification(errorMessage)
            }
        }
    }
}

def sendTelegramNotification(message) {
    def TELEGRAM_BOT_TOKEN = '6647136812:AAHMC_K0t8Swq5AK3W5XZ1jdgLtIETeEbXQ'
    def TELEGRAM_CHAT_ID = '1351870173'

    sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\":\"${TELEGRAM_CHAT_ID}\",\"text\":\"${message}\"}' https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage"
}

