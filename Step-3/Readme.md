# Csinálj egy application load balancert és target groupot

## 1
<details>
  <summary>Előkészületek megoldás</summary>

  ```
  https://console.aws.amazon.com/vpc/
  válassz ki kettő subnetet ami default subnet és különböző AZ-ban vannak, ÉS mindegyik legyen publikus (subneteknél lehet majd látni melyik az)
  
  
  
  ```
</details>

## 2
<details>
  <summary>Megoldás</summary>

  ```
  https://console.aws.amazon.com/ec2/
  In the navigation pane, choose Load Balancers.

Create Load Balancer.
Application Load Balancer.
internet-facing.
ipv4.
Add meg a két subnetet amit kiválasztottál.
security group jó az alap, ird fel az id-jét.
kettő listener kell mindkettő HTTP egyik legyen 80as port másik meg 8080 as.
Hozz létre 2 target groupot, ip-legyen a target legyen target-group-1 és target-group-2 a neve.

Elvileg megvagy:)

  ```
</details>
