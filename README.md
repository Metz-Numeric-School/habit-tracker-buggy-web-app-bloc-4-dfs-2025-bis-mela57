# My Habits Tracker (A Buggy Web Application)

# Présentation du projet

MyHabitTracker est une application web conçu sur une architecture MVC et qui s'inspire de l'arborsence et du fonctionnement du framework Symfony.

Celle-ci est destiné à être utilisée à des fins pédgogique uniquement et dans le cadre de la sensibilisation aux failles de sécurités les plus courantes sur le web.

## Téchnologies

- PHP 8.3
- MySQL 5.7

## Objectifs

Les objectifs sont les suivants :

* Prendre connaissance du code existant
* Paramétrer votre environnement dans le fichier .env ou .env.local
* 1ère partie (3h)
* * Préparer le déploiement de l'application (sur votre machine Debian) en rédigeant votre procédure dans le fichier `doc/DEPLOY.md`
  * Répondez aux questions figurant dans le fichier `doc/QUESTIONS.md`
* 2ème partie (2h)
  * Corriger toutes les failles de sécurité/bugs (voir `doc/TODO.md`) et déployez un correctif (toutes les failles ne sont pas répértoriées)
  * Pensez à mettre à jour le fichier `CHANGELOG.md`

## Lancement du projet

### Création de la base de données

```
php bin/create-database
```

### Lancement du serveur

Pour lancer le projet, vous devez impérativement passer par la commande : `php bin/serve`

### Création de la base de données

Pour créer la base de données vous pouvez lancer la commande : `php bin/create-database `

Un compte admin et utilisateurs seront également créés *(vous trouverez les informations dans le script database.sql)*

Ensuite, vous pouvez alimenter la base de données avec des données démo en lançant la commande : `php bin/load-demo-data`

## Livrables

Le code doit impérativement être push sur le repo GitHub Classroom qui vous a été assigné et sur la branche principale `main`

**!!! ATTENTION : la partie 2 ne sera pas évaluée si ce n'est pas le cas !!!**

# BONNE CHANCE


AApanel 
Nom de la base de données : sql_172_17_434
Nom d'utilisateur: sql_172_17_434
Mot de passe: e42392ba58dfc