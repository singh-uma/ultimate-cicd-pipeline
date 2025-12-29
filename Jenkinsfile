pipeline {
    agent any

    tools {
    jdk 'jdk21'
    maven 'maven3'
}

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''
                      ${scannerHome}/bin/sonar-scanner \
                      -Dsonar.projectKey=ultimate-cicd \
                      -Dsonar.projectName=ultimate-cicd \
                      -Dsonar.sources=.
                    '''
                }
            }
        }
    }
}

