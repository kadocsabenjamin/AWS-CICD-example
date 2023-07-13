# Step 5: Create your CodeDeploy application and deployment group (ECS compute platform)

## 1
### Create a CodeDeploy application
<details>
  <summary>Megoldás</summary>

  ```
CodeDeployt nyisd meg a console-ban
Csinálj egy Applicationt
adj neki nevet
Compute platform legyen Amazon ECS. 
  ```
</details>
## 2
### Create a CodeDeploy deployment group
<details>
  <summary>Megoldás</summary>

  ```
Ha megvan az 1. lépés akkor most lesz egy gomb hogy Create deployment group

adj neki nevet

Kell egy IAM role amit most el kell készíteni hogy működjön:
-lépj a consoleban az IAM hez,
-válaszd hogy "Roles"
-Create role
-AWS service
-use case legyen codeDeploy
codedeploy ECS
permission: AWSCodeDeployRoleForECS
name: pl CodeDeployECSRole

ezek után vissza a deployhoz

add meg az ARN-t (frissitsd az oldalt ha nem hozza ki)
válaszd ki a enviromental configokat
load balancert add meg

maradjon a routolás Reroute traffic immediately

meg is vagy:)
  ```
</details>
