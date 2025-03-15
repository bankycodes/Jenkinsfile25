pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven 3.8.5' // Set your installed Maven version
        JAVA_HOME = tool 'JDK 11' // Set your installed JDK version
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-repo/NumberGuessGame.git' // Change to your actual repo
            }
        }

        stage('Build & Compile') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean compile"
            }
        }

        stage('Unit Tests') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Code Quality Check') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn checkstyle:check"
            }
        }

        stage('Package WAR') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn package"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://localhost:8080/')], war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
