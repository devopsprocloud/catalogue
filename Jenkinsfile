pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        packageVersion = ''
        environment = ''
    }
    options {
        ansiColor('xterm')
        disableConcurrentBuilds()
    }
    stages {
        stage('Get the package version') {
            steps {
                script {
                def app_version = readJSON = 'package.json'
                packageVersion = app_version.version
                echo "Package Version: $packageVersion"
                }
            }
        }
    }
}