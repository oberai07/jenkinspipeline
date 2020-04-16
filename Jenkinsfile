pipeline {
    agent any
    environment {
        BRANCH_NAME = 'master'
    }
    options {
        timestamps()
    }
    triggers {
      pollSCM '* * * * *'
    }
    stages {
        stage ('Build & Deploy'){
            when {
                branch 'master'
            }
            steps {
                sh 'git pull origin master'
            }
        }
        stage ('Save Build') {
            input {
                  message 'Enter Path to save build?'
                  ok "Yes"
                  parameters {
                    string defaultValue: " Path ${env.WORKSPACE}/BuildNo.${env.BUILD_ID} ", description: 'Path to save the builds with timestamps', name: 'SAVE', trim: true
                  }
            }
            steps {
                sh "echo ${env.WORKSPACE}/BuildNo.${env.BUILD_ID}"
            }

        }
    }
}