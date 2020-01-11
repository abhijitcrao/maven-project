pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Stageing'){
            steps {
                Build job: 'deploy-to-staging'
            }
            post {
                success{
                    echo "Deploy to Stage enviornment is completed"
                }
            }
        }

    }
}