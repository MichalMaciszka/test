pipeline {
    agent {
        docker {
            image 'maven:3.8.6-openjdk-18'
        }
    }
    options {
        skipStagesAfterUnstable()
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
                sh 'mvn clean test' 
            }
            post {
                always {
                    archiveArtifacts artifacts: '/var/jenkins_home/workspace/test/target/surefire-reports/*.xml', fingerprint: true
                    junit(
                        allowEmptyResults: true,
                        testResults: '/var/jenkins_home/workspace/test/target/surefire-reports/*.xml'
                    )
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying..."
                sh 'mvn clean install -DskipTests'
            }
        }
    }
}
