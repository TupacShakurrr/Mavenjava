pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/TupacShakurrr/Mavenjava.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-creds',
                                          url: 'http://localhost:8081')],
                       war: 'target/Mavenjava.war',
                       contextPath: '/Mavenjava'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'curl http://localhost:8081/Mavenjava/'
            }
        }
    }
}
