# Test de performance
## 0. Lancement de Jmeter
Pour lancer le mode GUI de jmeter, allez dans votre terminal et lancez la commande suivante :

```console
jmeter
```

Vous devriez alors voir s'ouvrir une fenêtre. 
![[Pasted image 20220627183852.png]]
Renommez votre test plan en indiquant la date du jour et "Exercices JMeter"

## 1. Requête simple
Créer un nouveau Thread Group. 
Le renommer, et configurer pour 5 utilisateurs. 
Ajouter un ramp-up de 10 secondes.

Dans ce thread group, ajouter un sampler HTTP et le configurer pour votre site (si vous n'avez pas de site, vous pouvez utiliser https://voconsteroid.com. **Attention : si vous prenez un site publique, vous pourriez être poursuivi pénalement**).

Enfin, ajoutez un listener de type *View result tree*.

Vous pouvez maintenant lancer le test. 
Vérifiez grâce au listener le bon envoi des requêtes.

### Exercices Thread
Faites en sorte que le test ajoute 3 utilisateurs par secondes pendant 10 secondes.

Ajouter 4 loops et observez le résultat.

Question difficile : Faites en sorte de différer chaque requête de 300 millisecondes afin de simuler une utilisation humaine de votre site.

## Listeners
Ajouter un listener de type View Result Tree. Faites un test sur une requête, et observez les informations recueillies. Trouver l'onglet request header, c'est ici que vous pourrez voir les header de chaque requête.

Ajouter une visualisation du temps de réponse en graph, modifier l'intervalle à 500 millisecondes. Lancer un volume de 30 thread sur 15 secondes, et visualiser le résultat.

## Assertions
Ajouter une contrainte à votre requête : le temps réponse ne doit pas excéder 1 seconde.

Ajouter une seconde contrainte : le statut de la réponse doit être 200

## Header
Ajouter à vos requête le header suivant 'x-jmeter': 'true'. Visualiser ce header dans vos requêtes de test.
 