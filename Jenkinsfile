pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                //echo 'Building..'
                sh 'mvn clean build'
            }
        }
        stage('Test') {
            steps {
                //echo 'Testing..'
                sh 'mvn clean test'
            }
        }
        stage('Deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                //echo 'Deploying....'
                sh 'mvn clean install'
            }
        }
    }
}
