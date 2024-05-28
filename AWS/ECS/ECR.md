#### [Back](./README.md)

# Container Image for use on AWS ECS

AWS ECS Task definitions use docker image to launch containers on the container instance in your cluster.

## Create a docker image of a web application

1. Create Dockerfile
```bash
touch Dockerfile
```

2. Edit Dockerfile
```bash
FROM public.ecr.aws/amazonlinux/amazonlinux:latest
# Install dependencies
RUN yum update -y && \
    yum install -y httpd

# Install apache and write hello world message
RUN echo 'Hello World!' > /var/www/html/index.html
# Configure apache

RUN echo 'mkdir -p /var/run/httpd' >> /root/run_apache.sh && \
    echo 'mkdir -p /var/lock/httpd' >> /root/run_apache.sh && \
    echo '/usr/sbin/httpd -D FOREGROUND' >> /root/run_apache.sh && \
    chmod 755 /root/run_apache.sh

EXPOSE 80
CMD /root/run_apache.sh
```

3. Build Docker Image
```bash
docker build -t hello-world .
```

4. Run Docker Image
```bash
docker run -t -i -p 80:80 hello-world
```

# Push Docker Image to ECR(Elastic Container Registry)

1. Setup your aws Profile

2. Create an ECR Repo to store docker image.

```bash
aws ecr create-repository --repository-name hello-repository --region region --profile myaws
```

**output**
```json
{
 "repository": {
 "registryId": "aws_account_id",
 "repositoryName": "hello-repository",
 "repositoryArn": "arn:aws:ecr:region:aws_account_id:repository/hellorepository",
 "createdAt": 1505337806.0,
 "repositoryUri": "aws_account_id.dkr.ecr.region.amazonaws.com/hellorepository"
 }
}
```

3. Tag image with Repo URL
```bash
docker tag hello-world aws_account_id.dkr.ecr.region.amazonaws.com/hello-repository
```

4. Login to ECR Docker
```bash
aws ecr get-login-password --region region | docker login --username AWS --password-stdin aws_account_id.dkr.ecr.region.amazonaws.com
```

**Output**
```bash
Login Succeeded
```

5. Push the docker Image
```bash
docker push aws_account_id.dkr.ecr.region.amazonaws.com/hello-repository
```

