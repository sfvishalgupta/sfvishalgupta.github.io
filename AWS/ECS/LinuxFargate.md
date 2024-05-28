#### [Back](./README.md)

# Linux Container on AWS Fargate

1.  Create the Cluster

2.  Create a Task Definition
    Use below json to create new task definition with new revision

```json
{
    "family": "sample-fargate",
    "networkMode": "awsvpc",
    "containerDefinitions": [{
        "name": "fargate-app",
        "image": "public.ecr.aws/docker/library/httpd:latest",
        "portMappings": [{
            "containerPort": 80,
            "hostPort": 80,
            "protocol": "tcp"
        }],
        "essential": true,
        "entryPoint": ["sh","-c"],
        "command": [
            "/bin/sh -c \"echo '<html> <head> <title>Amazon ECS Sample App</title> <style>body {margin-top: 40px; background-color: #333;} </style> </head><body> <div style=color:white;text-align:center> <h1>Amazon ECS Sample App</h1> <h2>Congratulations!</h2> <p>Your application is now running on a container in Amazon ECS.</p> </div></body></html>' > /usr/local/apache2/htdocs/index.html && httpd-foreground\""
        ]
    }],
    "requiresCompatibilities": [
        "FARGATE"
    ], 
    "cpu": "256",
    "memory": "512"
}
```

3.  Create a Service with above task
4.  View your Service