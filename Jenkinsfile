pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }
    environment {
        DEBUG = 'true'
        appVersion = ''
    }

    stages {
        stage('Read the version') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"
                }
            }   
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Deploy') {
            when {
                expression { env.GIT_BRANCH == "origin/main" }
            }
            steps {
                sh 'echo This is Deploy'
            }
        }
    }

    post {
        always{
            echo "this section runs always"
            deleteDir()
        }
        success{
            echo "This section run when pipeline is success"
        }
        failure{
            echo "this section runs when pipeline is failure"
        }
    }
}