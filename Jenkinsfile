pipeline{
    agent{
        docker { image"kapilmodi/aws-agent:1.0"}
    }
    parameters{
        string(name: 'AWS_ACCESS_KEY', defaultValue: '', description: 'Enter here AWS ACCESS KEY ')
        password(name: 'AWS_SECRET_KEY', defaultValue: '', description: 'Enter here AWS SECRET KEY ')
        choice(name: 'Region', choices: ['us-east-1'], description: 'Enter the Region Name (Currently only 1 region available for demo)') 
        string(name: 'Cluster_Name', defaultValue: 'my-cluster', description: 'Enter here Kubernetes Cluster Name')
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
        stage("Creating Kubernetes Cluster"){
            steps{
                sh "eksctl create cluster --name ${params.Cluster_Name} --version 1.17 --region ${params.Region} --nodegroup-name linux-nodes --node-type t3.medium --nodes 2 --nodes-min 1 --nodes-max 3 --ssh-access --ssh-public-key HighLevelEkskey.pub --managed"
            }
        }
        stage("Create Deployments"){
            steps{
                sh "kubectl create namespace highlevel-prod"
                sh "kubectl get pods -n highlevel-prod"
                sh "kubectl apply -f http-version-1.yml"
                sh "kubectl get pods -n highlevel-prod"
                sh "kubectl get svc -n highlevel-prod"
                sh "kubectl apply -f http-version-2.yml"
                sh "kubectl get pods -n highlevel-prod"
            }
        }
        stage("Get Deployments"){
            steps{
                echo "Sleeping for 1 minute"
                sleep(time:1,unit:"MINUTES")
                echo "NOTE THE EXTERNAL IP OF THE 2 SERVICE"
                sh "kubectl get svc -n highlevel-prod"
                echo "TRY HITTING THE LOADBALANCER URL "
            }
        }
    }
}