pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/TupacShakurrr/Mavenjava.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-creds',
                                          url: 'http://localhost:8081')],
                       war: 'target/Mavenjava.war'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl http://localhost:8081/Mavenjava'
            }
        }
    }
}
