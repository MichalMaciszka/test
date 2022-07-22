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
            steps {
                //echo 'Deploying....'
                sh 'mvn clean install'
            }
        }
    }
}
