pipeline{
    agent{
        docker { image"kapilmodi/aws-agent:1.0"}
    }
    stages{
        stage("AWS Configure"){
            steps{
                sh "aws iam get-user"
            }
        }
    }
}