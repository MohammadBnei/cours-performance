# Exercice - Redaction d'un Plan

Réalisez cet exercice en choisissant 3 applications :
1. Un site avec un petit traffic (votre projet annuel, un site hyper-spécialisé, ...)
2. Un site avec un traffic moyen (media alternatif, blog...)
3. Un site avec un traffic important (twitter, google...)

## 1. Création d'un document
Créez un nouveau document au format de votre choix. Entrez sur une page de garde votre nom, prénom, classe et la date.

Donnez un titre à votre document, et inscrivez le nom de votre projet à tester.

Enfin, entrez les informations de votre groupe de travail.

## 2. Préambule
Dans une première section, nous allons décrire l'application qui va être testée. 

Entrez une description de votre projet, et l'objectif poursuivi par le test de performance.

La description doit contenir (liste non exhaustive) :
- Description globale du projet
- Objectif de l'application
- Type d'utilisateurs prévus
- Toute autre information que vous jugez pertinente

## 3. Architecture de l'application
Vous allez décrire ici l'architecture de votre application :
- Résumé de l'architecture globale
- Technologies/Langages utilisés
- Composants/Services  

Inclure un diagramme ou schéma décrivant les interactions entre les différentes parties de votre application.

Veuillez renseigner également l'infrastructure de production (heroku, conteneurisation, kubernetes...).

## 4. Exigences du test
En guise d'introduction à cette partie, indiquez la *justification* pour la création du test de performance (déterminer les capacités maximales de votre application, vérifier sa viabilité en production, détecter les goulots d'étranglement...).

Ensuite, inscrivez dans une table les différents processus non fonctionnels avec les informations suivantes :
- User Load (charge d'utilisateurs)
- Temps de réponse attendu
- Nombre de transactions / par heure

Par exemple :
| Business Transactions | User Load | Response Time | Transactions per hour |
|--------------|:-----------:|:------------:|:------------:|
| Access login page | 200 | 1 | 500 |
| Access register page | 100 | 1 | 300 |

## 5. Environnement de test
Précisez l'environnement dans lequel vont se dérouler les tests :
- CPU, Memoire
- OS
- Software pertinent

Comparez à l'environnement de production, et si possible calculer le coefficient proportionnel : si vous avez 2 CPU en prod, 1 seul pour les tests, alors vous aurez un coefficient de 0.5 (100 utilisateurs en prod reviennent à 50 utilisateurs pour l'environnement de test).

## 6. Planification des tests
L'objectif ici est de déterminer les besoins performatifs de votre application en production, de déterminer les métriques que vous souhaitez surveiller et les critères de réussite de votre test.

Pour cela, vous devrez :
1. Comprendre les limitations dues à l'architecture du projet et à l'infrastructure.
2. Comprendre/Prévoir le modèle de charge en production et l'adapter au modèle des tests.
3. Identifier les type de tests nécessaires en fonction de l'utilisation de l'application (spike, endurance, volume...)
4. Quels sont les métriques que l'on souhaite surveiller (utilisation du CPU/mémoire, temps de réponse moyen, taux d'erreur)
5. Quels sont les métriques qui définiront la réussite ou l'échec du test.

Consignez ces informations.

## 7. Etapes des tests
Détaillez les étapes des actions utilisateurs pour chaque process. Pour chaque script ainsi créé, un script de test de performance devra être réalisé.

Exemple :
| Step # | Business Process Name : Product Ordering |
|--------------|:-----------:|
| 1 | Home Page |
| 2 | Login |
| 3 | Search Product |
| 4 | Select Product |
| 5 | Payment |
| 6 | Logout |

En fonction des process choisis, établissez les jeux de données nécessaires. Prodiguez les détails sur le type de données, leur quantité et leur provenance (clone de la prod, fichiers csv créés uniquement pour ce test par exemple).

Séparez les jeux de données internes aux process (clés API, credentials, ...) et ceux externes (remplissage de la base de donnée).

Indiquez comment se fait la préparation de la donnée.

## 8. Execution des tests
En premier lieu, détaillez le nombre de cycles d'execution de chaque process. 
Ajoutez un résumé du scénario de test.

Exemple :

| Test Run | Test Scenario Summary |
|--------------|:-----------:|
| Smoke Test | To validate the performance test scripts and monitors |
| Cycle 1 - Run 1 | Load Test - 1 Hour test with peak load |
| Cycle 1 - Run 2 | Repeat Load Test - 1 Hour test with peak load |
| Cycle 1 - Run 3 | Stress Test - 1 Hour test with 150% of peak load |
| Cycle 2 - Run 1 | Load Test - 1 Hour test with peak load |
| Cycle 2 - Run 2 | Repeat Load Test - 1 Hour test with peak load |
| Cycle 2 - Run 3 | Stress Test - 1 Hour test with 150% of peak load |

Ensuite, détaillez chaque scénario comme l'exemple suivant (pour le Load Test) :

|  | Test Details |
|--------------|:-----------:|
| **Purpose** | Peak hour transaction processing will be under examination to <br/> determine if the system can maintain response times <br/> under the highest anticipated load. <br/> This test is designed to collect performance <br/> metrics on transaction throughput, response times, <br/> and system resource utilization, <br/> in comparison to Performance requirements. |
| **No. of Tests** | 4 (2 tests per cycle) |
| **Duration** | Ramp-up: X - Steady State: X - Ramp-down: X |
| **Scripts** | 1. XXXX - 2. XXXX |
| **Scenario Name** | Load Test Scenario |
| **User Load / Volume** | 500 Vusers (Threads) Load |
| **Entry Criteria** | 1. The code should be stable and functionally verified <br/> 2. Test Environment should be stable and ready to use <br/> 3. Test Data should be available <br/> 4. All the NFRs should be agreed with the project <br/> 5. Test scripts should be ready to use |
| **Validation Criteria** | 1. The mean of the response time should be below 1.5 sec <br/> 2. The error rate should be below 5% |

## 9. Résultats des tests
Ici, référencez les graphiques et données résultant des tests effectués

## 10. Analyses et Optimisations proposées
Après avoir effectué une comparaison entre les résultats obtenus et ceux escomptés, analyser les résultats et tentez de proposer des axes d'amélioration. Ceux-ci peuvent être :
- Optimisation d'un service grâce a de meilleurs algorithmes
- Optimisation de l'infrastructure (scalabilité accrue par exemple)
- Détection d'éventuels goulots d'étranglements
 