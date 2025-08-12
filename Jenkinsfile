pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    // environment {

    // }
    options {
        ansiColor('xterm')
        disableConcurrentBuilds()
    }
    stages {
        stage('Initial Step') {
            step {
                echo "This is the first step"
            }
        }
    }
}