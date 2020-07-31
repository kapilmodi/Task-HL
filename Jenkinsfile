pipeline{
    agent{
        docker { image"kapilmodi/aws-agent:1.0"}
    }
    parameters{
        string(name: 'AWS_ACCESS_KEY', defaultValue: '', description: 'Enter here AWS ACCESS KEY ')
        password(name: 'AWS_SECRET_KEY', defaultValue: '', description: 'Enter here AWS SECRET KEY ')
        choice(name: 'Region', choices: ['us-east-1'], description: 'Enter the Region Name (Currently only 1 region available for demo)') 
    }
    environment
    {
        AWS_ACCESS_KEY_ID="${params.AWS_ACCESS_KEY}"
        AWS_SECRET_ACCESS_KEY="${params.AWS_SECRET_KEY}"
        AWS_DEFAULT_REGION="${params.Region}"
    }
    stages{
        stage("AWS Configure"){
            steps{
                sh "aws iam get-user"
            }
        }
    }
}