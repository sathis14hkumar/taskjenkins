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
        
        post {
                failure {
                    echo "Checkout failed!"
                    sendTelegramNotification("Checkout failed!")
                }
        }
        
    }
    }
 post {
        success {
            script {
                // Send success notification to Telegram
                sendTelegramNotification("Pipeline Passed!")
            }
        }
        failure {
            script {
                // Send failure notification to Telegram
                sendTelegramNotification("Pipeline Failed!")
            }
        }
    }
}

def sendTelegramNotification(message) {
    def TELEGRAM_BOT_TOKEN = '6647136812:AAHMC_K0t8Swq5AK3W5XZ1jdgLtIETeEbXQ'
    def TELEGRAM_CHAT_ID = '1351870173'

    sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\":\"${TELEGRAM_CHAT_ID}\",\"text\":\"${message}\"}' https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage"
}
