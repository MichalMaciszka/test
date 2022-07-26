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
                sh 'mvn test' 
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml' 
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
