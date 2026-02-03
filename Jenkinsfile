pipeline {
    agent any

    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    environment {
        DOCKERHUB_USER = "Gowri0126"
        IMAGE_NAME     = "maven-simple"
        IMAGE_TAG      = "1.0"
        FULL_IMAGE     = "gowri032/maven-simple:1.0"
    }
    triggers{
        cron(*/1 * * * *)
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',url: 'https://github.com/Gowri0126/maven-simple.git'
                    credentialsId: 'github-tocken'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify JAR') {
            steps {
                sh 'java -jar target/maven-simple-1.0-SNAPSHOT.jar'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t maven-simple:1.0 .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'Docker-jenkins-PAT',
                    usernameVariable: 'gowri032',
                    passwordVariable: 'g123456789'
                )]) {
                    sh '''
                        echo "g123456789" | docker login -u "gowri032" --password-stdin
                    '''
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push maven-simple'
            }
        }
    }

    post {
        success {
            echo "✅ Image pushed to Docker Hub: maven-simple:1.0"
        }
        always {
            sh 'docker logout || true'
        }
    }
}
