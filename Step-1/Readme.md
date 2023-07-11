## 1
### Csinálj egy image-t (nginx imgae lesz majd a példában javaslom hogy azt csinálj)
<details>
  <summary>Megoldás</summary>

  ```
  Lépj be az EC2 instance-ba és add ki ezt a parancsot:
  docker pull nginx

  Majd ezzel tudod ellenőrizni milyen image-eid vannak:
  docker images
  ```
</details>

## 2
### Töltsd fel az ECR repo-ba a kész image-et ami csak lokálisan van

<details>
  <summary>Megoldás</summary>

  ```
  aws ecr create-repository --repository-name nginx

  Ha minden jól ment ez a kapott output:
  {
    "repository": {
        "registryId": "aws_account_id",
        "repositoryName": "nginx",
        "repositoryArn": "arn:aws:ecr:us-east-1:aws_account_id:repository/nginx",
        "createdAt": 1505337806.0,
        "repositoryUri": "aws_account_id.dkr.ecr.us-east-1.amazonaws.com/nginx"
    }
  }
  ```
</details>

## 3
### Tageld meg az imaget az előző lépés outputjából megkapott "repositoryUri"-val

<details>
  <summary>Megoldás</summary>

  ```
  docker tag nginx:latest aws_account_id.dkr.ecr.us-east-1.amazonaws.com/nginx:latest
  ```
</details>

## 4
### Futtasd az aws ecr get-login-password parancsot a helyes régió és vpc id-vel

<details>
  <summary>Megoldás</summary>

  ```
  aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 111122223333.dkr.ecr.us-west-2.amazonaws.com/nginx
  ```
</details>

## 5
### Told fel a repóba a helyes "repositoryUri"-val

<details>
  <summary>Megoldás</summary>

  ```
  docker push 111122223333.dkr.ecr.us-east-1.amazonaws.com/nginx:latest
  ```
</details>
