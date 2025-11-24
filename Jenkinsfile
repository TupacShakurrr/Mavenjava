pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Public repo, no credentials needed
                git branch: 'main',
                    url: 'https://github.com/TupacShakurrr/Mavenjava.git'
            }
        }

        stage('Build with Maven') {
            steps {
                // Windows-friendly Maven build
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Deploy using the Deploy to Container plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat-creds',
                                          url: 'http://localhost:8081')],
                       war: 'target/Mavenjava.war',
                       contextPath: '/Mavenjava'
            }
        }

        stage('Verify Deployment') {
            steps {
                // Use absolute path to curl.exe so Jenkins finds it
                bat '"C:\\Tools\\curl-8.17.0_4-win64-mingw\\curl-8.17.0_4-win64-mingw\\bin\\curl.exe" --fail http://localhost:8081/Mavenjava/"
            }
        }
    }
}
