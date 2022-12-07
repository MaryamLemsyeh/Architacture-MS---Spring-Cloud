# Objectifs : 

Créer une application basée sur une architecture micro-service qui permet de gérer les factures contenant des produits et appartenant à un client.

# Consignes : 

1.Créer le micro-service customer-service qui permet de gérer les client

2.Créer le micro-service inventory-service qui permet de gérer les produits

3. Créer la Gateway Spring cloud Gateway avec une Configuration statique du système de routage

4. Créer l'annuaire Eureka Discrovery Service

5. Faire une configuration dynamique des routes de la gateway

6. Créer le service de facturation Billing-Service en utilisant Open Feign

7. Créer un client Web Angular (Clients, Produits, Factures)

8. Déployer le serveur keycloak :
     - Créer un Realm
     - Créer un client à sécuriser
     - Créer des utilisateurs
     - Créer des rôles
     - Affecter les rôles aux utilisateurs
     - Tester les différents modes d'authentification avec Postman en montrant les contenus de Access-Token, Refresh Token 

9. Sécuriser les micro-services et le frontend angular en déployant les adaptateurs Keycloak

# Outils : 

Spring cloud.

Intellij.

Navigateur de choix.

# Démarrer le projet :

-Clôner le projet sur la repositoy : https://github.com/MaryamLemsyeh/Architacture-MS---Spring-Cloud
-Démarrer les applications.
-Démarrer l'outil d'enregistrement Eureka Discovery Client.

# Explications et captures d'écran :

Créer le gatway qui va essayer de dispatcher les requettes vers les bons microservices.
##Méthode 1 :
pour configurer le gateway on peut utiliser un fichier de format .yml
![actuator 2](https://user-images.githubusercontent.com/105390951/206061225-90217f05-acfc-42f3-a0e2-61465400336b.PNG)
![beansactuator1](https://user-images.githubusercontent.com/105390951/206061219-63bd5439-a761-4512-aa20-d7690c86440a.PNG)
![CUSTOMER](https://user-images.githubusercontent.com/105390951/206061217-0f91bba4-8501-4f05-95d3-4fb8f32773b1.PNG)
![customers](https://user-images.githubusercontent.com/105390951/206061214-51b5166c-4505-4b32-97b7-6e11165b99fd.PNG)
![products 1](https://user-images.githubusercontent.com/105390951/206061212-27af264b-1fe0-47ea-b763-f9b5858d570e.PNG)

## Méthode 2 : 
on peut utiliser une configuration java, 
on créer une classe de configuration, une méthode qui retourne un bean (objet route locator) pour configurer les routes, ila  besoin d'un objet en parametres qui s'appelle route locator builder, 
On a BEOSIN d'un rapidAPI countries c'est une service public connaissant l'adresse on peut l'utiliser, il est un service externe qui ne s'enregistre pas sur discovery.
on utilise le service d'enregistrement, on demande au service de s'enregistrer et on essaye de faire la gestion de maniere dynamique mais en exploitant le log balancer.
lorsqu'on utilise la configuration statique y'a pas de log balancer, si on a plusieurs instance du même microservice on peut pas l'utiliser.
![gateway products](https://user-images.githubusercontent.com/105390951/206061287-fda189d4-c4c2-4a25-8522-49de63a78fac.PNG)
![gateway customers](https://user-images.githubusercontent.com/105390951/206061289-d83d2596-5ee3-4fb1-aa97-9d5eda7e58e6.PNG)
![customers gateway java](https://user-images.githubusercontent.com/105390951/206061280-ffbcb390-443f-4690-bca1-e23d184c7aed.PNG)
![gateway prod java](https://user-images.githubusercontent.com/105390951/206061284-789679f2-f3f6-466c-a85c-79f6f7d48ea2.PNG)
![enable eureka all](https://user-images.githubusercontent.com/105390951/206061277-b518c321-e3b9-4e3f-a1ac-5ae20aa86ebc.PNG)

## Méthode 3 : 
on créer eureka server, pour activer eureka server il faut utiliser l'annotation EnableEurekaServer, on démarre.
on active spring.cloud.discovery.enabled sur true, on trouve 3 microservices enregistrés, customer-service, product-service et gateway-service.
dans gateway on modifie la configuration , au lieu de localhost, on utilise que le nom du microservice , lb = log balancer.
![products lb gateway](https://user-images.githubusercontent.com/105390951/206061484-3c307aae-9f2f-469c-b9fc-70c85caf90b9.PNG)
![customers gateway lb](https://user-images.githubusercontent.com/105390951/206061496-f8dd13ef-347d-4089-8098-349dcd694c56.PNG)
![customers url discovery](https://user-images.githubusercontent.com/105390951/206061502-ae019372-0ddf-4b80-80df-5933e3e49848.PNG)
![discovery products url](https://user-images.githubusercontent.com/105390951/206061504-4c03e830-4f10-42bb-a44f-d2c4fdd4d1a4.PNG)

Ajouter billing-service :
Créer class client sous billing-service, quand je consulte un customer, openfile deserialize, prend les données JSON et les stock dans objet. faut garder les mêmes nom sinon on ajoute des annotations JACKSON pour faire la correspondance entre les 
avoir le detail sur les produits et clients, on utilise OpenFeign qui permet de communiquer avec les microservices via rest.
![customer1](https://user-images.githubusercontent.com/105390951/206061536-d34c5dc3-8784-4828-924c-8685ea700c71.PNG)
![product1](https://user-images.githubusercontent.com/105390951/206061541-c4342635-9604-420f-af98-a80eef3f0603.PNG)


 
