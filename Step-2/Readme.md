# Create task definition and AppSpec source files and push to a CodeCommit repository

https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_execution_IAM_role.html

## 1. 
### Csinálj egy task definitiont az imagedhez.
<details>
  <summary>Megoldás</summary>

  ```
  Kell egy taskdef.json file. Image-nek, add meg az image nevet, pl: nginx.

  Javaslom aki ismeri a vi-t használja azt, de a vim,nano és bármi más is ugyan úgy jó.
  ```
</details>
<details>
  <summary>Megoldás kód</summary>

  ```
  fontos!:az acclount ID-t írd át!
  
  {
    "executionRoleArn": "arn:aws:iam::account_ID:role/ecsTaskExecutionRole",
    "containerDefinitions": [
        {
            "name": "sample-website",
            "image": "nginx",
            "essential": true,
            "portMappings": [
                {
                    "hostPort": 80,
                    "protocol": "tcp",
                    "containerPort": 80
                }
            ]
        }
    ],
    "requiresCompatibilities": [
        "FARGATE"
    ],
    "networkMode": "awsvpc",
    "cpu": "256",
    "memory": "512",
    "family": "ecs-demo"
  }
  ```
</details>

## 2. 
### Regisztáld be a taskdef filet az ecs-be
<details>
  <summary>Megoldás</summary>

  ```
  megjegyzés: az hogy "file://" az KELL oda, és nyilván ha kell adjunk meg hosszabb elérési utat.

  aws ecs register-task-definition --cli-input-json file://taskdef.json
  ```
</details>

## 3. 
### Ird át a taskdef-ben hogy ne konkrét image legyen megadva hanem általános "image placeholder"
<details>
  <summary>Megoldás</summary>

  ```
  long console output here
  ```
</details>
## 4. 
### AppSpec.yaml file létrehozása a következő lépés
<details>
  <summary>Így néz ki az általános AppSpec file template:</summary>

  ```
version: 0.0
Resources:
  - TargetService:
      Type: AWS::ECS::Service
      Properties:
        TaskDefinition: "task-definition-ARN"
        LoadBalancerInfo:
          ContainerName: "container-name"
          ContainerPort: container-port-number
# Optional properties
        PlatformVersion: "LATEST"
        NetworkConfiguration:
            AwsvpcConfiguration:
              Subnets: ["subnet-name-1", "subnet-name-2"]
              SecurityGroups: ["security-group"]
              AssignPublicIp: "ENABLED"
Hooks:
- BeforeInstall: "BeforeInstallHookFunctionName"
- AfterInstall: "AfterInstallHookFunctionName"
- AfterAllowTestTraffic: "AfterAllowTestTrafficHookFunctionName"
- BeforeAllowTraffic: "BeforeAllowTrafficHookFunctionName"
- AfterAllowTraffic: "AfterAllowTrafficHookFunctionName"
  ```
</details>
<details>
  <summary>Megoldás</summary>

  ```
  version: 0.0
  Resources:
    - TargetService:
        Type: AWS::ECS::Service
        Properties:
          TaskDefinition: <TASK_DEFINITION>
          LoadBalancerInfo:
            ContainerName: "sample-website"
            ContainerPort: 80
  ```
</details>
## 5. 
### Told fel a CodeCommit repoba (ezt elvileg már létre kellett hoznod, ha nem tedd meg most)
<details>
  <summary>Megoldás</summary>

  ```
  long console output here
  ```
</details>
