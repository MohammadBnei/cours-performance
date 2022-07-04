# Test de Performance

## Introduction
Le test de performance est un processus de test logiciel qui a pour but de tester la vitesse, le temps de réponse, la stabilité, la fiabilité, la scalabilité, et l'utilisation des ressources d'une application en fonction d'une charge de travail spécifique.

Il a 2 buts principaux :
- Identifier les goulots d'étranglement d'une application
- Vérifier que l'application puisse répondre aux besoins de vitesse, scalabilité et stabilité de son utilisation.

### Pourquoi tester la performance
En tant qu'ingénieur logiciel, votre objectif est de développer de nouvelles fonctionnalités. Cependant, il n'y aura aucun impact sur le produit si vos fonctionnalités ne sont pas viables en production, ou si elles plantent sous une charge forte. Il est donc nécessaire d'assurer une délivrance optimale malgré des conditions diverses, afin de proposer la meilleure expérience utilisateur possible. 

Il est également primordial de connaître les capacités performatives de votre application : les charges maximales, le temps de réponse moyen en fonction de conditions précises... qui donneront à l'entreprise une prévisibilité accrue.

Enfin, la détection de goulots d'étranglement permet de définir les points faibles de votre système, et donc les zones où des efforts de développement seront nécessaire.

## Les différents types de test

### Load Testing
On va chercher avec le Load Testing à vérifier si l'application peut endurer une utilisation normale et anticipée. Nous garderons un oeil sur les temps de réponse et le taux d'erreurs.

C'est le test de performance basique.

### Stress Testing
On cherche a connaître les points de rupture de l'application pour identifier les métriques maximums.
Généralement, nous partirons d'une charge normale. Puis, de façon graduelle, nous augmenterons cette charge jusqu'à ce que l'application ne puisse plus répondre.
Il est important de comprendre pourquoi et comment le système plante, quels sont les différents points de rupture et s'il arrive a se remettre en route par la suite sans intervention humaine.

### Spike Testing
On vas tester ici une montée subite en charge. Sur un temps court, on envoie une charge importante pour simuler une arrivée massive d'utilisateurs.
A la différence du Stress Testing, l'objectif n'est pas de crasher l'application. On souhaite déterminer si celle-ci peut supporter un type d'utilisation spécifique.

### Volume Testing
On veut savoir si les performances de l'application sont impactées par le volume de données en base. Pour cela, on insère un volume très important dans la base de données, et on teste avec du Load Testing.

### Endurance Testing
On cherche à connaître la résilience de l'application sur un temps long (8h/16h/24h). On détecte les fuites de mémoires, les baisses de performance en fonction du temps, et globalement la stabilité du système.  

# Métriques
-   **Processor Usage –** an amount of time processor spends executing non-idle threads.
-   **Memory use –** amount of physical memory available to processes on a computer.
-   **Disk time –** amount of time disk is busy executing a read or write request.
-   **Bandwidth –** shows the bits per second used by a network interface.
-   **Private bytes –** number of bytes a process has allocated that can’t be shared amongst other processes. These are used to measure memory leaks and usage.
-   **Committed memory –** amount of virtual memory used.
-   **Memory pages/second –** number of pages written to or read from the disk in order to resolve hard page faults. Hard page faults are when code not from the current working set is called up from elsewhere and retrieved from a disk.
-   **Page faults/second –** the overall rate in which fault pages are processed by the processor. This again occurs when a process requires code from outside its working set.
-   **CPU interrupts per second –** is the avg. number of hardware interrupts a processor is receiving and processing each second.
-   **Disk queue length –** is the avg. no. of read and write requests queued for the selected disk during a sample interval.
-   **Network output queue length –** length of the output packet queue in packets. Anything more than two means a delay and bottlenecking needs to be stopped.
-   **Network bytes total per second –** rate which bytes are sent and received on the interface including framing characters.
-   **Response time –** time from when a user enters a request until the first character of the response is received.
-   **Throughput –** rate a computer or network receives requests per second.
-   **Amount of connection pooling –** the number of user requests that are met by pooled connections. The more requests met by connections in the pool, the better the performance will be.
-   **Maximum active sessions –** the maximum number of sessions that can be active at once.
-   **Hit ratios –** This has to do with the number of [SQL](https://www.guru99.com/sql.html) statements that are handled by cached data instead of expensive I/O operations. This is a good place to start for solving bottlenecking issues.
-   **Hits per second –** the no. of hits on a web server during each second of a load test.
-   **Rollback segment –** the amount of data that can rollback at any point in time.
-   **Database locks –** locking of tables and databases needs to be monitored and carefully tuned.
-   **Top waits –** are monitored to determine what wait times can be cut down when dealing with the how fast data is retrieved from memory
-   **Thread counts –** An applications health can be measured by the no. of threads that are running and currently active.
-   **Garbage collection –** It has to do with returning unused memory back to the system. Garbage collection needs to be monitored for efficiency.

## Processus
Nous définissons ici une méthodologie de création d'un plan de test de performance. 

### 1. Conditions
Il est primordial d'identifier l'environnement de test et celui de production.  En effet, les performances varient grandement en fonction du hardware, de l'OS, des logiciels sous jacents et du réseau. 

Une application pourra fonctionner de façon optimale sur votre machine de développement (si vous avez le dernier macbook m1 pro, une configuration de gamer...) mais sous performer sur l'environnement de prod limité à un seul CPU et 2 GB de ram.

Egalement, selon les paramètres réseau, vous pourriez vous retrouver avec un environnement localisé aux US et donc observer une latence importante en France.

Enfin, les considérations logicielles (OS, conteneurisation, Kubernetes...) doivent être connues et comprises.

### 2. Critères 
Nous définissons ensuite les critères d'acceptation de notre test. 
Cela inclut les objectifs et contraintes de débit, temps de réponse et allocation de ressources. 

Il est important de connaitre les besoins fonctionnels de l'applications en terme d'utilisateurs et d'utilisation attendues. Certains projets ont des besoins très spécifiques (génération de fichiers, connexion longue durée, chat...) et les tests doivent intelligemment prendre en compte les aspérités du projet.

### 3. Planification et Design
Après avoir définit ce que nous voulons tester, il faut maintenant définir comment nous allons effectuer les tests.
Quels vont être les scénarios clés afin de tester, selon les critères, tous les use-cases pertinents. 
Il est nécessaire de simuler une variété d'utilisateurs, planifier les données utilisées par les tests de performances et choisir les métriques à faire ressortir.

### 4.  Configuration de l'environnement
Nous devons préparer l'environnement dans lequel vont se dérouler les tests. Il est préférable que cet environnement soit au plus proche de la prod, au niveau hardware, software, et topologie réseau.

### 5. Implémentation
Sur l'outil choisit ([jmeter](https://jmeter.apache.org)), nous pouvons maintenant implémenter les scénarios planifiés en amont. Les étapes sont les suivantes :
- Avoir les jeux de données prêtes
- Avoir les credentials prêts
- Implémenter les scénarios de tests voulus, et les ordonner
- Avoir la configuration des endpoints, certificats et path nécessaires

### 6. Execution
Executer les tests en surveillant les résultats et si possible l'utilisation des ressources de l'environnement de test.

### 7. Analyse, Tune & Retest
Consolider, analyser et partager les résultats. Ensuite, modifier les tests légèrement afin de détecter une amélioration ou une détérioration des performances. 
Par exemple, si on cherche à connaître les performances maximales d'une application, alors les itérations de tests viendront à chaque fois augmenter (ou abaisser) la charge jusqu'à obtenir une valeur précise. 


## Rédaction du Plan de test de Performance
Voir les exercices.
[Template](https://drive.google.com/file/d/159NXKUT4O9xfiD1j6iUuZhNG0Eq97AHP/view)
[Example](https://qatestlab.com/assets/Uploads/QATestLab-Performance-Test-Plan.pdf)

## Outils du Test de Performance
Nous allons utiliser 2 outils pour réaliser nos scénarios de tests, les executer et généré des résultats.

Le premier, principal, est [jmeter](https://jmeter.apache.org). 100% Java et open source, ce programme très complet a été augmenté grâce à des plugins créés par la communauté.

Le second est [blazemeter](https://www.blazemeter.com). Il permet l'enregistrement d'actions utilisateur sur un site afin de les reproduire dans un scénario de test jmeter (ou sur le cloud).

### Jmeter
Nous allons ici présenter différents éléments de jmeter. Pour chacun des ces éléments, nous décrirons très largement leur utilité.

### GUI mode

![[Pasted image 20220627183852.png]]
Comme montré ci-dessus, jmeter se compose de plusieurs parties :
- Les éléments de votre plan de test
- La configuration des éléments de votre plan
- Les options (enregistrer, ouvrir un plan, configuration de jmeter...)

Lorsque vous sélectionnez un élément de votre plan (dans le rectangle de gauche), la page de configuration de cet élément s'affiche dans l'encadré de droite. Nous pouvons alors lui donner un nom et le paramétrer.

Une bonne utilisation de jmeter est de créer ses plans de tests avec le mode graphique, puis d'utiliser le terminal pour les lancer.

### Thread
![[Pasted image 20220627184654.png]]
Les threads sont le nombre d'utilisateurs qui va être utilisé pour nos tests. 

Nous pouvons dès lors paramétrer notre Thread Group avec les options suivantes : 
1. **Action to be taken after a sampler error:** Si une erreur survient, le plan doit-il continuer, démarrer la prochaine itération, arrêter le thread, graceful shutdown ou quitter.
2. **Thread Properties:** 
	1. Number of threads (Users) : Le nombre d'utilisateurs que le test va utiliser.
	2. Ramp-Up period : le temps de montée en charge (si 10 utilisateurs et ramp-up de 10 secondes, le thread ajoutera 1 utilisateur chaque seconde)
	3. Loop count : nombre de répétitions du thread 

### Sampler
![[Pasted image 20220627185528.png]]
Les sampler sont les éléments de requêtage. Nous choisissons un type de requête (http, grpc, soap...) et nous pouvons la configurer avec les valeurs correspondant au serveur que nous souhaitons tester.

Les samplers sont liés au Thread Group.

### Listeners
![[Pasted image 20220627191106.png]]
Les listeners nous permettent d'afficher le résultat des samplers. Nous pouvons ici définir les retours pertinents (latence, byte out, nombre d'erreurs).

Un listener particulier est le *sample data writer*. En lui donnant le chemin d'un fichier, il pourra y écrire les résultats du test au format csv.

### Assertions
Les assertions valident les réponses obtenues. Nous pouvons définir par exemple un temps de réponse maximal, et lorsqu'une requête mettra un temps supérieur à celui définit alors cette requête génèrera une erreur.

### Variables
JMeter nous donne la possibilité d'utiliser des variables dans quasiment tous les champs de configuration de tous les éléments. Une variable s'écrit sous la forme ${NOM_DE_LA_VARIABLE}. Cette variable sera automatiquement remplacée lors de l'execution du test.

A noter qu'avec la même syntaxe, nous pouvons implémenter des fonctions (ex: *${\_\_intSum(2,3)}*, avec 2 "\_")

### Config Element
Ces élément de configuration permettent comme leur nom l'indique de configurer notre test. Outre les configurations classiques (HTTP header, cookie manager...), nous pouvons importer des données de test depuis un fichier CSV (*CSV data set config*). Cela peut s'avérer utile si l'on veut pouvoir se connecter avec différents utilisateurs prédéfinis, ou si notre application nécessite des options particulières pour pouvoir être testée. 

### Post Process
Avec les outils de post process, vous pouvez extraire des réponses des données. Ces données pourront être réinjectées dans les requêtes suivantes grâce aux variables jmeter.

### JMeter CLI
jmeter -n → cli mode
-t "test file location" 
-l "test result location"
-e -o "output folder"

```bash
CURRENT_TIME=$(date "+%Y-%m-%d-%H-%M-%S")

#Script Location with Name

SCRIPT=my_script.jmx

# CSV results

FOLDER=$SCRIPT_$CURRENT_TIME

RESULT=$FOLDER/result.csv

LOG=$FOLDER/logs.log

HTML=$FOLDER/html-report

  

jmeter -n -t $SCRIPT -l $RESULT -j $LOG -e -o $HTML
```
