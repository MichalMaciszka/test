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
                    archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
                    junit(
                        allowEmptyResults: true,
                        skipPublishingChecks: true,
                        testResults: '**/target/surefire-reports/*.xml'
                    )
                }
                failure {
                    mail bcc: '',
                        body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '',
                        charset: 'UTF-8', from: '',
                        mimeType: 'text/html', replyTo: '',
                        subject: "ERROR CI: Project name -> ${env.JOB_NAME}",
                        to: "mmaciszka@griddynamics.com";
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
