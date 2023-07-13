
# Create your Amazon ECS cluster and service



## 1
### ECS cluster
<details>
  <summary>Megoldás</summary>

  ```
  https://console.aws.amazon.com/ecs/
  Clusters.
  Create cluster.
  Adj nevet
  Create.
  
  ```
</details>

## 2
### Service
<details>
  <summary>Megoldás</summary>

  ```
  Vissza az EC2-be

Csinálj egy JSON filet: create-service.json.

Fontos, ne bemásold és menj tovább, NEM fog működni.
Ki kell cserélni pár dolgot:
-taskDefinition nek meg kell adni valami, pl "ecs-demo:1"
-cluster: ide a cluster nevet add meg
-targetGroupARN ezt írd be (megtalálod az ec2-consolban)
-subnetek, ide azt a két subnetet amit korábban megkellett nézned
-security group, ide ird be a sg-t amit megadtál a load balancernek.

ha ezek jók működnie kellene.

{
    "taskDefinition": "family:revision-number",
    "cluster": "my-cluster",
    "loadBalancers": [
        {
            "targetGroupArn": "target-group-arn",
            "containerName": "sample-website",
            "containerPort": 80
        }
    ],
    "desiredCount": 1,
    "launchType": "FARGATE",
    "schedulingStrategy": "REPLICA",
    "deploymentController": {
        "type": "CODE_DEPLOY"
    },
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-1",
                "subnet-2"
            ],
            "securityGroups": [
                "security-group"
            ],
            "assignPublicIp": "ENABLED"
        }
    }
}
  ```
</details>

## 3
### Service feltöltés és ellenőrzés
<details>
  <summary>Megoldás</summary>

  ```
ha igy hagyod akkor "my-service" lesz a neve
  aws ecs create-service --service-name my-service --cli-input-json file://create-service.json

ezzel tudod ellenőrizni hogy létrejött e:
aws ecs describe-services --cluster cluster-name --services service-name

ha esetleg hibát kapsz elleőrizd hogy a cluster és service név is megegyezik!
  ```
</details>

