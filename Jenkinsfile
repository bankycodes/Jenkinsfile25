pipeline {
    agent any
    tools {
        maven 'Maven'  // Uses Jenkins-configured Maven
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/bankycodes/NumberGuessGame.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sh 'scp -i ~/bankole.pem target/*.war ec2-user@54.159.16.237:/opt/tomcat/webapps/'

stage('Deploy to EC2') {
    steps {
        sh 'scp -o StrictHostKeyChecking=no -i /var/lib/jenkins/bankole.pem target/NumberGuessGame-1.0-SNAPSHOT.war ec2-user@54.159.16.237:/opt/tomcat/webapps/'
    }
}
                
            }
        }
    }
}
