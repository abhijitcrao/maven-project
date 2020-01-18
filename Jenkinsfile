pipeline{
    agent any
    stages{
        stage('Build'){

            steps{
                sh 'mvn clean package'
                sh "docker build . -t tomcatweb:${env.BUILD_ID}"
            }
        }

    }
}