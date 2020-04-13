pipeline {
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    stages {
        stage ('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://gitlab.com/kagarwal0205/sampleproject.git']]])
            }
        }
        stage ('Save Build') {
            input {
                  message 'Enter Path to save build?'
                  ok "Yes"
                  parameters {
                    string defaultValue: '$WORKSPACE/BUILD_ID', description: '', name: 'BUILD', trim: true
                  }
            }
            steps {
                echo "${BUILD}"
            }
        }
    }
}