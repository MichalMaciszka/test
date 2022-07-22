pipeline {
    agent {
        docker {
            image 'maven:3.8.6-openjdk-18'
            args '-v /root/.m2:/root/.m2' 
        }
    }

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
