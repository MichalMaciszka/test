pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo Building'
//                 echo 'Building..'
                sh 'mvn clean build'
            }
        }
        stage('Test') {
            steps {
                sh 'echo Testing...'
//                 echo 'Testing..'
                sh 'mvn clean test'
            }
        }
        stage('Deploy') {
            when {
                expression {
                    sh 'echo Expression...'
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
//                 echo 'Deploying....'
                sh 'echo Deploying...'
                sh 'mvn clean install'
            }
        }
    }
}
