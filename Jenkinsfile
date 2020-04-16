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
                git 'https://gitlab.com/kagarwal0205/sampleproject'
                lastChanges since: 'LAST_SUCCESSFUL_BUILD', format:'SIDE',matching: 'LINE'
                sh 'chmod +x ./changes.sh'
                sh './changes.sh'
            }
        }
        stage ('Save Build') {
            input {
                  message 'Enter Path to save build?'
                  ok "Yes"
                  parameters {
                    string defaultValue: " /tmp/${env.BUILD_ID} ", description: 'Path to save the builds with timestamps', name: 'SAVE', trim: true
                  }
            }
            steps {
                sh "echo ${env.WORKSPACE}/BuildNo.${env.BUILD_ID}"
            }

        }
    }
}