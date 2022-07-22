pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'mvn clean build'
            }
        }
        stage('Test') {
            steps {
                echo "Executor number: ${env.EXECUTOR_MUBER}"
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
                echo "JAVA_HOME: ${env.JAVA_HOME}"
                sh 'mvn clean install'
            }
        }
    }
}
