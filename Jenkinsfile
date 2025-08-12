pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        packageVersion = ''
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }

    stages {
        stage('Get the version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "application version: $packageVersion"
                }
            }
        }
        stage('Installing Dependecies') {
            steps {
                sh """
                    npm install 
                """
            }
        }
        stage('List the contents') {
            steps {
                sh """
                    ls -la 
                """
            }
        }
        stage('Zipping the contents') {
            steps {
                sh """
                    zip -r catalogue.zip ./* -x "*.zip" -x ".git"
                """
            }
        }

        // stage('Check Parameters') {
        //     steps {
        //         echo "Hello ${params.PERSON}"

        //         echo "Biography: ${params.BIOGRAPHY}"

        //         echo "Toggle: ${params.TOGGLE}"

        //         echo "Choice: ${params.CHOICE}"

        //         echo "Password: ${params.PASSWORD}"
        //     }
        // }
    }
    //POST Stages
    post { 
        // always { 
        //     echo 'Pipeline is executed'
        // }
        failure {
            echo 'The pipeline is Failed, Please send some alerts'
        }
        success {
            echo 'Pipeline executed successfully'
        }
    }
}
