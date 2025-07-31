pipeline {
    agent any
    
     triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Piyushjangid01/Vishwakrma-Furniture.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image"
                sh 'docker build -t vishwakrma-furniture .'
            }
        }

        stage('Docker Login and Push') {
            steps {
                echo "Logging into DockerHub and pushing image"
                sh 'docker login -u piyushj01 -p Piyush@0001'
                sh 'docker tag vishwakrma-furniture piyushj01/vishwakrma-furniture:latest'
                sh 'docker push piyushj01/vishwakrma-furniture:latest'
            }
        }
    }

    post {
        success {
            mail to: 'piyushjangid7417@gmail.com',
                 subject: "Jenkins Build #${env.BUILD_NUMBER} Successful",
                 body: """
Build Successful

Project: vishkakrma-furniture
Build Number: ${env.BUILD_NUMBER}
View Build Log: ${env.BUILD_URL}console
"""
        }

        failure {
            mail to: 'piyushjangid7417@gmail.com',
                 subject: "Jenkins Build #${env.BUILD_NUMBER} Failed",
                 body: """
Build Failed

Project: vishkakrma-furniture
Build Number: ${env.BUILD_NUMBER}
View Build Log: ${env.BUILD_URL}console
"""
        }
    }
}
