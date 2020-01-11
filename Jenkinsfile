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
                build job: 'deploy-to-staging'
            }
            post {
                success{
                    echo "Deploy to Stage enviornment is completed"
                }
            }
        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve Production Changes ?'
                }
                build job: 'deploy-to-prod'
                post {
                    success{
                        echo "Deploy to Production completed succesfully"
                    }
                    failure{
                        echo "Deployment to PROD got failed, Please verify steps"
                    }
                }

            }
        }

    }
}