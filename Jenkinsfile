pipeline {
    agent any
    environment {
      BUILD_PATH = "$WORKSPACE/repo-"${BUILD_ID}""
    }
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
                    string defaultValue: '${BUILD_PATH}', description: '', name: 'BUILD', trim: true
                  }
            }
            steps {
                echo "${BUILD_PATH}"
                echo "${BUILD}"
            }

        }
    }
}