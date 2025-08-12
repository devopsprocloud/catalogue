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
        stage('Installing NodeJS') {
            steps{
                sh """
                    sudo dnf module disable nodejs -y
                    sudo dnf module enable nodejs:20 -y
                    sudo dnf install nodejs -y
                    sudo dnf install zip -y
                """
            }
        }
        stage('Installing Dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
        stage('Zipping the Artifact') {
            steps {
                sh """
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                """
            }
        }
        stage('List the contents') {
            steps {
                sh """
                    ls -ltr
                """
            }
        }
    }
}