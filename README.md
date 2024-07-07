# QuizApplication
Simple Quiz application - Deployment in Docker / AWS - Elastic Kubertnetes Service

# Prequisites :
AWS account has to be created and Docker Desktop, aws CLI, Kubectl CLI and eksctl CLI to be installed.

Setting up the application in Local:
1. Open Docker desktop
2. Run the command for build from the code directory path : docker build -t quizApplication:v1 .
3. Run the command - docker images ( This should get the image which you bulit in step 2).
4. Run the docker image by the command :  docker run -d -p 80:80 quizApplication:v1
5. Open the browser with the url : http://localhost/quiz.html

Deploying the application in AWS - Elastic Kubernetes Service:
1. Open your AWS account concole and Search for Elastic Container Registry
2. Create a repository with name "quizApplication" and mark it private and then click on the repository.
3. In the new page  - you will get to see View Push commands and follow the steps and this will upload the docker image to the AWS - Elastic Container Registry. After uploading the image get the image URI and note it down. 
4. Next will create the cluster by the command -  eksctl create cluster --name quiz-cluster --version 1.28 --nodes=1 --node-type=t2.small --region us-east-2. This will create the cluster with 1 node. This may take some time.
5. Next from the AWS console - Search for AWS - Elastic Kubertnetes Service. View the custer created.
6. Edit the k8s.yaml with the image uri copied from step 3 in the line no : 17
7. Then run the kubectl command - kubectl apply -f k8s.yaml
8. This will complete the deployment
9. To check the deploymnet run the below 2 command
    1.  kubectl get pods ( This command will show all pods running - 3 pods should be running as we have menitioned 3 replicas in k8s.yaml)
    2.  kubectl get service (This command will show all the services -  copy the External ip which would be domain for the URL to run the application)
    3. open the browser with the url http://<External-IP>/quiz.html



