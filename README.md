

# Qualité de développement

Le but de ce cours est de faire des tests tests unitaires et d'intégration au fur et à mesure que des nouveaux composants sont intégrés dans une apllication tout en vérifiant que les tests précédents continuent de passer sans relever d'erreur. 

On appelle cela des tests de non regression.

## Support de cours

https://drive.google.com/drive/folders/1RVLc4yg5IKTq3OSht6wm1Cdjq9jOLEqy?usp=sharing




>**Ressource de M. LEMAIRE:**
>
> [Introduction au cours de qualité de développement](https://e.pcloud.link/publink/show?code=XZRFxPZxa6jVeLys40yTU3p3RaEzXaheXuk=)



# TD 1 - JUnit

JUnit est un framework de tests unitaires pour le langage de programmation Java, créé par Kent Beck et Erich Gamma.

Etudier un exemple de classe de Test : https://junit.org/junit5/docs/current/user-guide/#writing-tests

Etudier l'utilisation des assertions : https://junit.org/junit5/docs/current/user-guide/#writing-tests-assertions


>**Ressource de M. LEMAIRE:**
>
>[Tests unitaires avec JUNIT](https://e.pcloud.link/publink/show?code=XZc4tPZdNNzQHJT3vLYNlEYQGR70JHMaPj7)



# TP 1 :  JUnit, développent et tests unitaires de la classe métier

## Création du projet

* Tests unitaires avec JUNIT

1. Créer un projet avec Intellij :

<img src="images/projet.png" width="500"/>

Attendre que le projet soit créé.

2. Mise en place du framewok pour les tests unitaires 

2.1. Ajouter la librairie Jupiter (clic droit sur le projet -> Open Module Settings) : 

<img src="images/librairie.png" width="500"/>




2.2. Configuration du projet

* Ajouter dans le dossier `src` deux dossiers (java pour les *classes à tester* et test pour les *classes de test*).

* Indiquer à Intellij que java est le dossier pour le code source et test celui pour les tests.

<img src="images/dossier.png" width="500"/>

3. Commençons le développement

3.1. En ce qui concerne la classe métier  `Voiture`

* Créer une classe `Voiture` dans le packe de `src/main/java`

> Les caractéristiques de d'une *voiture* sont la *marque* (`String`) et le *prix* (`Float`) et une plaque d'imatriculation sous la forme `XXXYYZZ` où :
> * `XXX` sont trois chiffres,
> * `YY` sont deux lettes en majuscules,
> * `ZZ`sont deux chiffres.

Toute anomalie sera signalée par une `RunTimeException` de type `IllegalStateException`.

3.2. En ce qui concerne la classe de test pour la clasee métier `Voiture`

* Créer une classe `VoitureTest` dans le package de `src/test/java` et écrivez le code de test de la classe Voiture en utilisant le framework JUnit 5

> Le but est de tester l'interface publique de la classe métier `Voiture` et de vérifier que l'objet est dans un état valide.

Lancer le programme de test (clic droit sur la classe de test)

> Tous les tests doivent passer (*être vert*)


# TP2 : Intégration continue, développement et tests unitaires de la classe service

**Faisons le point :**  Au début de cette partie vous avez écrits et fait passé tout vos tests unitaires
  
Quelques exemples de tests unitaires : 

<img src="images/voituretest.jpg" width="600"/>



## Etape 1 : Appropriation du projet


Vous devez vous appropier ce projet, c'est-à-dire que **vous devez le déplacer vers un dépôt Git vous appartenant**.



>**Ressource de M. LEMAIRE:**
> Support de cours concernant Git
> [Support de cours sur Git](https://e.pcloud.link/publink/show?code=XZT45CZgsA2bvsKBefHmVhdgo3G9mlfDa3y)
>
>[Création d'un dépôt Git](https://e.pcloud.link/publink/show?code=XZ3qthZaMGfUQCtTUR1zXO0O5jqnQVf5lQX)


## **Voici quelques indications :**

1. Créer votre dépôt distant

<img src="images/creation_depot_distant.jpg" width="600"/>

**Notes :**
* Le dépôt doit-être privée dans le cadre de ce travail pratique.
* Le dépôt doit-être vide car nous allons l'initialiser avec notre dépôt local
    * ne pas cocher `Add a README file`
    * ne pas ajouter de fichier `.gitingnore`
   
2. Déplacez-vous dans le dossier contenant votre projet sur votre machine

<img src="images/deplacement_dans_projet_local.jpg" width="1000"/>


3. Initialiser votre dépôt distant avec votre dépôt local (ici c'est un exemple avec **mon** dépôt distant !)

```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/bouchaiblemaire/r402_2025_qual_dev.git
git push -u origin main
```

Si nécessaire supprimer le lien avec l'origine existante : 
```
git remote remove origin
```

et refaire le `git add remote`.

**Affichage obtenu avec mon dépôt :**

<img src="images/init_remote_guhub_repository.jpg" width="800"/>




4. Inscrivez votre enseignant comme *participant* de votre projet github.


## **Etape 2 : Collaborer à un projet : le concept du pull request**

**Le principe :**

* Quand un développeur apporte une modification au code il faut tester que son code n'est pas buggé et qu'il ne provoque pas d'erreur dans le code existant (test de non regression du code).

**Règle :** Pour ne pas corrompre le code existant, **toutes modifications doit se faire dans une branche**.

* Le développeur en question va pousser sa branche vers le serveur distant Git et à ce moment-là les tests (de son code et du code déjà écrit) doivent être déclenchés **automatiquement côté serveur** :
    * Si les tests réussissent, le chef de projet (ou une personne autorisée) pourra alors fusionner les branches et les autres développeurs pourront alors télécharger la dernière version du code.
  
Cette procédure qui part de l'initiative du développeur et qui se termine par la fusion des branches par le chef de projet si les tests réussissent est appelée *pull request*.

### Comment les test tests sont automatisées côté serveur ? 

#### Github actions

Côté serveur, Github peut exécuter des tâches automatiquement comme lancer les tests. Pour cela **il faut configurer une action**.


### **En ce qui concerne un développeur de l'équipe de projet**

Quand un développeur collabore à un projet il procède de la façon suivante : 

1. le développeur récupère le projet sur sa machine (`git clone`)
    * Il créer un dépot local dans sa machine
  

**Remarques :** 
* Pour ce travail pratique vous disposez déjà du dépôt local ! 
* Vous pouvez jouer le rôle d'un nouveau développeur à clonant le dé^pot distant dans un aitre dossier de votre machine locale.

2. le développeur créé une copie du projet afin de ne pas affecter le code qui est déjà en production (`git branch` et `git checkout`)

Exemple :

```
git branch newcarservice
git checkout newcarservice
```

ou en une seule commande :
```
git checkout -b newcarservice
```

**Note :** Vous le ferez dans la partie *développement de la couche service*


* Toutes modifications se font sur une branche et n'altère pas le projet principal (branche `main`)

3. Le développeur travaille à débogger le code ou à développer une nouvelle fonctionnalité (`git add`, `git commit`)
    * Dans cette étape, **toutes les modifications se font dans la branche locale**.
  
4. Le développeur écrit aussi les programmes de tests qui valident son travail
   
5. Et enfin le développeur envoie sa copie du code vers le serveur distant git pour partager ses midifications/ajouts (git push)



### **En ce qui concerne le chef de projet**

Le chef de projet peut alors déclencher un processus d'**intégration continue** (CI) en lançant les procédures de tests écrit par le développeur :
> c'est le pull request. Un script va alors être déclanché sur un serveur de test. 

Si les tests du développeurs sont concluants, le chef de projet peut alors décider de fusionner la copie du développeur avec la version originale (`git marge`).
* Tous les développeurs doivent alors récupérer la mise à jour du code sur leur machine en faisant un `git pull`

Et c'est là qu'on comprend le terme *pull request* qui est finalament une demande de pull faite par un développeur au chef de projet quand il a finit son travail.

**En conclusion :** Dès lors que le code est testé sur les serveurs de github, le code est disponible auprès des autres développeurs de l'équipe.



### Voici les étapes que nous allons effectuer pour le développement de la couche service de l'application**

**A lire jusqu'au bout AVANT DE COMMENCER !**

#### **A. Travail à faire par le chef de projet,  mise en place du processus d'intégration contenue**

1. Connectez-vous sur votre dépôt distant en utilisant l'interface Web de Github et cliquez sur le bouton `Actions`

<img src="images/mise_en_place_actions_pull_request_etape_1.jpg" width="800"/>

2. Cliquez sur le bouton configure de la tuile `Java with Gradle`

**Note :** Prendre soin de bien lire les informations qui sont affichées !

<img src="images/mise_en_place_actions_pull_request_etape_2.jpg" width="600"/>

**Lisez et interprétez les informations qui sont affichées dans le script affiché !**

Cliquez sur le bouton `Commit changes`

<img src="images/mise_en_place_actions_pull_request_etape_3.jpg" width="400"/>


* Votre *action* est mis en place et est lancé 
  * c'est à dire que tous les tests seront automatiquement lancé à chaque demande de *pull request* ! 
* Soyez patient et interpréter les résultats et corriger les erreurs eventuelles.
    * Pour cela cliquez sur le lien du *workflow* affichée

<img src="images/mise_en_place_actions_pull_request_etape_4.jpg" width="600"/>

*Indices sur quelques solutions pour corriger certaines erreurs éventuelles :*
* Activez les *dépendances de graphes* dans la paramètres avancées de votre dépot git distant.
* Donnez les droits d'execution au script `gradelew` et mettre à jour le dépôt distant.

Dans l'exemple suivant, l'erreur de droit d'exécution sur le fichier `gradlew` a été corrigé et une autre demande de pull request a été effectuée :
* Le chef de projet à effacé le premier workflow pour garder ke deuxime
  
  
<img src="images/mise_en_place_actions_pull_request_etape_5.jpg" width="600"/>

A ce point du travail pratique le `workflow`doit s'exécuter sans erreur et **tous les indicateurs doivent être vert**.


#### **B. Travail à faire par le développeur, écriture de la couche service**

Nous allons dans cette étape écrire la couche service et faire un demande de *pull request* pour rajouter cette couche au projet principal sur le serveur Git distant.

Nous supposons avant de commencer cette étape que :
* Vous avez créee et initialisé votre **dépôt distant**, une seule branche `main` existe.
* Vous avez mis en place correctement les mécanismes d'intégration continue.

Votre projet contient :
* La classe métier `Voiture` dans le fichier java `Voiture.java`
* La classe de tests `VoitureTest` dans le fichier java `VoitureTest.java`


1. Créer une nouvelle branche sur votre machine locale:
```
git branch newcarservice
```
2. Se déplacer vers la nouvelle branche:
```
git checkout newcarservice
```
3. Ajouter les fonctionnalités de la couche service ainsi que les tests unitaires associés (voir plus loin *développement de la couche service*).
   
4. Faire passer tous les tests, ils doivent être tous vert.
   
5. Mettre à jour le dépôt local en *committant* les modifications :
```
git add .
git commit -a -m "newcarservice"
```
6. Se remettre sur la branche `main` de votre dépôt local
```
git checkout main
```
7. Envoyer les changements vers GitHub :
```
git push -u origin newcarservice
```

**Remarque :** Une demande de *pull request* sera ouverte aytomatiquement.


#### **C. Travail à faire le chef de projet, traiter la demande de pull request**

A partir de là, vous jouez le rôle d'un chef de projet.

1. Traiter le demande de *pull request*
2. Accépter (dans le cas du travail pratique)  la demande de *pull request*
  * la fusion de la nouvelle branche avec la branche `main` est effectuée (`git merge`)

> Sur toutes les machines des développeurs (y-compris celle du développeur qui a soumis son code) afin de mettre à jour la branche main sinon le serveur Github n'acceptera pas de nouveau push au pretexte que le code n'est pas à jour
>```
>git pull origin main
>```


3. La nouvelle branche peut alors être effacée sur la machine du développeur et cell qui est chez Github :

```
git branch -D newcarservice
```
```
git push origin --delete newcarservice
```



### **Mise en pratique !**


**Développement de la couche service**

**1. Ce que doit faire le développeur**

Coder une classe de service en implémentant l'interface suivante :

```java
package fr.r402.service;
import fr.r402.metier.Voiture;

public interface IStatistique {

    public void ajouter(Voiture voiture);

    /**
     * Calcul d'un prix dégressif en fonction du nombre de voitures :
     * 5% de remise supplémentaire sur chaque voiture à chaque fois que 5 voitures sont ajoutées
     * et une remise maxi de 20 000 euros.
     * @return le prix des voitures
     * @throws IllegalStateException s'il n'y a pas de voiture
     */
    public double prix() throws IllegalStateException;


    /**
     * Retourne la voiture à la position i
     * @param i position de la voiture en retourner
     * @return (Voiture)
     * @throws IndexOutOfBoundsException : Aucune voiture à la position indiqué
     */
    public Voiture getVoiture(int i) throws IndexOutOfBoundsException;
}
```


Etudiez la technique de la matrice de test dans le cours sur les tests : https://drive.google.com/drive/folders/1RVLc4yg5IKTq3OSht6wm1Cdjq9jOLEqy?usp=sharing

Etablir la matrice de tests.

Ajouter à votre projet les tests définis dans la matrice de tests.


1. Dessinez le diagramme de classes de l'application à cette étape.
2. Ecrire la classe service `Statistique`qui implémente l'interface `IStatistique`.
3. Ecrire la classe de tests.
4. Lancez et faire passer les tests.
5. Faire une demande de *pull request* au chef de projet.


**2. Ce que doit faire le chef de projet :**

1. Traiter la demande de *pull request*

<img src="images/pull_request_pending.jpg" width="800"/>

2. Vérifier que la fusion est possible :

<img src="images/pull_request_pending_able_to_merge.jpg" width="600"/>

3. Créer la demande de *pull request*
   
<img src="images/pull_request_create_pull_request.jpg" width="600"/>

4. Vérifier que tous les tests automatisés passent avant d'accepter de fusionner la branche `newcarservice`avec la branche `main`
  * Tous les indicateurs doivent être au vert



<img src="images/pull_request_merge.jpg" width="600"/>


**Après traitement de la demande de pull request**

La nouvelle branche peut alors être effacée sur la machine du développeur et cell qui est chez Github :

```
git branch -D newcarservice
```
```
git push origin --delete newcarservice
```

**3. Ce que doit faire le développeur**

Mettre à jour sa branche `mail`

```
git pull
```


# TP 3

Etude du framework de test inclus dans les projets Spring boot : https://github.com/charroux/springbootest

Etude du framework de test Mockito: https://github.com/charroux/mockito




## Présentation de l'application

L'application à développer contient : 

- une base de données.
- un service Web

L'application est programmée en Java avec le framework Spring Boot (pour faciliter l'accès à la base de données ainsi 
que le développement du service web).

Le but de l'application est de faire des statistiques sur des voitures.

## Récupération du projet

L'application dont vous lisez le Readme actuellement ne vous appartient pas (vous n'êtes pas les proprétaires du dépôt git).
Cependant, vous pouvez télécharger ce projet sur vos machines et ensuite l'uploader vers un de vos dépôts git.

>**Ressource de M. LEMAIRE:**
>Voici un tutoriel vidéo qui est suivie de la procédure détaillée commande par commande :
>
>[Tutoriel github]( https://e.pcloud.link/publink/show?code=XZ3qthZaMGfUQCtTUR1zXO0O5jqnQVf5lQX)


Si vous n'avez pas utilisé Github depuis un moment, il se peut que le Token qui vous permet d'accéder à Github soit périmé.
Dans ce cas, il faudra en génbérer un autre. La procédure est indiqué ici : https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
Il faudra alors utiliser ce token à la place de votre mot de passe quand vous ferrez des commandes git.

Démarrer le machine de l'école sous Linux.

Attention ! sur les machines de l'IUT il faut se placer sur `/tmp` car cela ne fonctionne pas sur les dossiers personnels.
```
git clone https://github.com/charroux/qualiteDeDeveloppement
```
Se placer ensuite dans le dossier du projet:
```
cd qualiteDeDeveloppement
```
## Copie du projet dans un dépôt git qui vous appartient

Durant les TP vous allez travailler en binôme. Créez un dépôt de code public mais vide dans Github (sans Readme, ni gitignore),
puis recopier ce projet dans votre dépôt git en prodédant comme suit :
```
rm -rf .git
git init
git add *
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/[adresse .git de votre projet]
git push -u origin main
```

## Edition du projet

### Avec Intellij
Lancer Intellij et ouvrir tout simplement le projet. 
Cependant, sur les machines de l'IUT, la compilation du projet ne fonctionnera pas. 
Ce n'est pas très génant pour compiler votre projet vous pourrez ke faire via une commande.

### La phase de build incluant l'exécution des tests
Le build du projet (se compilation) ainsi que le lancement des programmes de tests peuvent se faire en ligne de commend via  la commande: 
```
./gradlew build
```
Une vidéo de démonstration : https://e.pcloud.link/publink/show?code=XZIwqhZkSSA8vXtyWmbn0aEKkgsrJ5QBxlX

Le consultation du rapport de test ce fait ici : build/reports/tests/test/index.html

### Avec Eclipse 
La version Eclipse de l'IUT n'ayant pas le plugin gradle, il n'est pas recommandé de l'utiliser.

## Codage des classes de données, accès à la base de données

### Codage d'une classe Voiture

Une ébauche de la classe Voiture est donnée : https://github.com/charroux/qualiteDeDeveloppement/blob/main/src/main/java/com/example/demo/data/Voiture.java

Elle contient déjà un identifiant qui va servir de clef primaire à une table dans la base de données (explications à venir).

Ajoutez à cette classe les attributs :
 - une marque
 - un prix
 
### Tests unitaires de la classe Voiture
Le dossier src/test/java contient déjà l'ébauche de la classe de test de la voiture. 
Cette classe de test est appelée VoitureTest. Ajoutez à cette classe autant de méthodes que vous jugez utile pour 
tester la classe Voiture. Vérifiez que les méthodes de la classe Voiture retournent les résultats attendus en utilisant la classe Assert du framework Spring dont voici la documentation :

https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/Assert.html

Sous Linux :
```
./gradlew build
```
Vérifier le rapport de test: build/reports/tests/test/index.html

# TP 3

## La base de données
La base de données est HSQLDB. Elle s'exécute "En mémoire" pour ne pas avoir à démarrer un serveur de base de données tant qu'on est en mode développement.
En conséquence, les données sont perdues dès que l'application s'arrête.

## Cours sur l'accès à la une base de données en Java
https://drive.google.com/drive/folders/1RVLc4yg5IKTq3OSht6wm1Cdjq9jOLEqy?usp=sharing

## Accès à la base de données
Pour permettre d'accéder par programmation à la base de données uns interface a déjà été programmée : https://github.com/charroux/qualiteDeDeveloppement/blob/main/src/main/java/com/example/demo/data/VoitureRepository.java

Un exemple d'utilisation de cette interface est données dans le cours sur l'accès à la base de données. 

Pour connaître l'ensemble des méthodes d'accès à la base de données, 
étudier l'interface CRUD repository : https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html

## Test de l'accès à la base de données
Les tests à réaliser ici vont utiliser le framework de test Mockito : https://github.com/charroux/mockito

Le dossier src/test/java (package data) contient l'ébauche du programme de test de la base de données :
https://github.com/charroux/qualiteDeDeveloppement/blob/main/src/test/java/com/example/demo/data/BaseDeDonneesTests.java

Ajoutez à cette classe autant de méthodes que vous jugez utile pour tester l'accès à la base de données. 

# TP 4 : codage de la classe de service qui intègre la base de données

L'application a développer sur la base des voitures calcule des statistiques sur les voitures.
La base de cette application est une interface : https://github.com/charroux/qualiteDeDeveloppement/blob/main/src/main/java/com/example/demo/service/Statistique.java

## Coder une classe de service

Coder une classe qui implémente cette interface.
La classe Echantillon doit retourner le nombre de voiture et leur prix moyen.

Pour que cette classe puisse accéder à la base de données il suffit d'y ajouter :

```
@Autowired
VoitureRepository voitureRepository;
```

## Tests de la classe de service

Créer un package appelé service pour tester la classe de service et implementez-y un programme de test.

# TP 5 : codage de l'interface Web

## Cours sur les Web services Rest
https://drive.google.com/drive/folders/1RVLc4yg5IKTq3OSht6wm1Cdjq9jOLEqy?usp=sharing

## Codage d'un Web service

Ajouter au dossier src un package appelé web.

Coder une classe controller qui réagit à deux requêtes HTTP : 
- GET sur /statistique et qui retourne un objet du type échantillon
- POST qui permet d'ajouter une nouvelle voiture

## Test du Web service

Créer dans le dossier test un package web. Implentez-y une classe de test pour le Web service.


**Sujet de M. CHARROUX révisé et complété par B. LEMAIRE dans le cadre des séances de travaux dirigés et pratiques de la ressource R402**
