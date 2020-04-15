pipeline {
    agent any
    options {
        timestamps()
    }
    triggers {
      pollSCM '* * * * *'
    }
    stages {
        stage ('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://gitlab.com/kagarwal0205/sampleproject.git']]])
            }
        }
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
                    string defaultValue: '${env.WORKSPACE}/BuildNo.${env.BUILD_ID}', description: 'Path to save the builds with timestamps', name: 'SAVE', trim: true
                  }
            }
            steps {
                sh 'echo ${env.WORKSPACE}/BuildNo.${env.BUILD_ID}'
            }

        }
    }
}