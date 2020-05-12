pipeline {
    agent any
    options {
        timestamps()
    }
    environment {
        SAVEDIR = '/root/output'
    }
    triggers {
      pollSCM '* * * * *'
    }
    stages {
        stage ('Checkout'){
           steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Github', url: 'https://github.com/oberai07/jenkinspipeline.git']]])
            }
        }
        stage ('Save Build') {
            input {
                  message 'Enter Path to save build?'
                  ok "Yes"
                  parameters {
                    string defaultValue: "${SAVEDIR}/BuildNo.${env.BUILD_ID}", description: 'Path to save the builds with timestamps', name: 'SAVE', trim: true
                  }
            }
            steps {
                sh ' mkdir $SAVE '
            }
        }
    }
}