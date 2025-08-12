pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        packageVersion = ''
        nexusUrl = '98.83.155.227:8081'
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }

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
                    sudo yum install zip -y
                """
            }
        }
        stage('Zipping the contents') {
            steps {
                sh """
                    zip -q -r catalogue.zip ./* -x "*.zip" -x ".git"
                """
            }
        }
        stage('Uploading Artifacts') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusURL}",
                    groupId: 'com.roboshop',
                    version: "${packageVersion}",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
           }   
       }
        stage('Build Job') {
            steps {
                build job: "catalogue-deploy", wait: true,
                parameters: [
                    string(name: 'version', value: "${packageVersion}"),
                    string(name: 'environment', value: 'UAT')
                ]
            }
        } 
    }
    post { 
        always { 
            echo 'Deleting the directory'
            deleteDir()
        }
        failure {
            echo 'The pipeline is Failed, Please send some alerts'
        }
        success {
            echo 'Pipeline executed successfully'
        }
    }
}
