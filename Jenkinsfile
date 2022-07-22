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
                echo "Building..."
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') { 
            steps {
                echo "Testing..."
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
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
