# Kubernetes - Deployment (AWS EKS)

## Useful Links

- [Amazon AWS EKS](https://aws.amazon.com/eks/)

-----------------

docker build -t nikhilchandan/kub-dep-users:latest .
docker push nikhilchandan/kub-dep-users

docker build -t nikhilchandan/kub-dep-auth:latest .
docker push nikhilchandan/kub-dep-auth

docker build -t nikhilchandan/kub-dep-tasks:latest .
docker push nikhilchandan/kub-dep-tasks

-------------------
# A. Configure cluster
1. create cluster on AWS (eg kub-dep-demo )
2. kubernetes version configure
3. cluster service role 
5. manage permision with IAM console
6. create role and assign user roles
7. create permission for EKS services
8. select case EKS cluster ( predefined role ) and proper name and role
9. on cluster config select the above role created

# B. Specify Networking
1. configure network for cluster 
2. services -- Aws cloud formation -- create stack --- add default
3. copy url AWS S3 Url  https://s3.us-west-2.amazonaws.com/amazon-eks/cloudformation/2020-10-29/amazon-eks-vpc-private-subnets.yaml 
4. Specify stack name, add tags and leave defaults  -- create stack ( create a VPC network )
5. Specify networking by selecting the above created networking service others are default
6. cluster endpoint access ( public and private )

# C. Configure Logging -- Done

# D. Configure EKS > Cluster > Kub-dep-demo > Add Node Group
1. Add node name, Add IAM roles 
2. IAM console -- create role - AWS service --- ec2 ---permissions -- ( eksworker node policy , add ec2 container registery(readonly) , eks cli policy ) [ for image pulling etc ]
3. Node IAM Role -- select above created role 
4. Node group compute configuration 
    - AMI type ( Amazon linux 2 ) 
    - intance type ( t3. micro ) [ larger the powerfull ]
    - disk size ( 20 gb )
5. Node Group scaling configuration ( not similar as pods, more nodes more spaces to be distributed for pods )
    - minimum size (2 nodes)
    - maximum size (2 nodes)    
    - desired size (2 nodes)
6. Networking to default -- create ( will take some time to build )

--------------------------

# How we send commands locally 

C:\Users\nikhil.chandan\.kube\config
this config kubectl connects to minikube

---------------------------

# Send commands to EKS cluster

1. AWS command line interface (windows installer, mac avaliable)
2. my security  -- create a security access key -- download file and save it ( AWSAccessKeyId, AWSSecretKey )
3. 'aws configure' command
4. enter AWSAccessKeyId and enter AWSSecretKey and enter default region name
5. aws eks --region us-east-2 update-kubeconfig --name --cluster name ( this is let talk to the created to AWS EKS cluster)
5. Inspect file C:\Users\nikhil.chandan\.kube\config we will get the AWS config file

--------------------------

# apply local yaml files

1. kubectl apply -f=auth.yaml -f=users.yaml
2. kubectl get deployments, pods, services
3. kubectl get services ( will give the url for created services )

-------------------------

# persistent volume in EKS

1. Aws efs csi ( https://github.com/kubernetes-sigs/aws-efs-csi-driver )
   kubectl apply -k "github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.2"
   kubectl apply -k "github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/dev/?ref=master"
2. AWS EC2 -- create security group -- vps ( eks vpc )
   Inbound rule -- add rule --  NFS - custom source -- sider range -- copy IPv4 CIDR to custom
   Outbound rule same -- create 
3. AWS console - AWS Elastic file system - create file system -- select eks-vpc 
4. EFS > File system > create --- choose created security group -- create
5. copy file system ID and apply to users.yaml 




















