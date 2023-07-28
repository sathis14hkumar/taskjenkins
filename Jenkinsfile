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
          }
          }
