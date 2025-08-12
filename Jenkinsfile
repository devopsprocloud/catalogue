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
                def packageJSON = readJSON file: 'package.json'
                packageVersion = packageJSON.version
                echo "Application Version: $packageVersion"
                }
            }
        }
    }
}