<H2> Docker Images </H2>

kapilmodi/highlevel:1.0      -> First Version of the code

kapilmodi/highlevel:2.0      -> Second Version of the code

kapilmodi/aws-agent:1.0      -> Agent which have basic tools installed like aws,kubectl,etc..


<H2> How To Run </H2>

1) Create a Jenkins pipeline and give the path of the repo <B>Jenkinsfile</B>. 

2) Build the Jenkins pipeline 

3) Enter your aws credentials and k8s cluster name

4) First it will deploy a kubernetes cluster and then will deploy both versions of the code

5) Note the load balancer Endpoint for both the service deployments

6) Now go to your DNS Management portal (In my case it is route53) 

7) Add a new <B>Weighted Record</B>. Give the following values

    a) Type: A
       Endpoint: ###FIRST LOADBALANCER ENDPOINT FROM STEP 5
       Weight: 7
    b) Type: A
       Endpoint: ###SECOND LOADBALANCER ENDPOINT FROM STEP 5
       Weight: 3

8) Save Changes

9) Try hitting the url. 