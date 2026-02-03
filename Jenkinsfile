pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Gowri0126/maven-simple.git'
            }
        }
        stage('Maven Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Maven Run') {
            steps {
                sh 'java -cp target/simple-maven-1.0-SNAPSHOT.jar com.example.App'
            }
        }
    }
}
