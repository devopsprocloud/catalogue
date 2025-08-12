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
            steps {
                echo "This is the first step"
            }
        }
    }
}