# Procédure de Déploiement
## Préparation du VPS
## Méthode de déploiement

Décrivez ci-dessous votre procédure de déploiement en détaillant chacune des étapes. De la préparation du VPS à la méthodologie de déploiement continu.

## 1. Configuration initiale du projet

### Étapes après avoir cloné le projet

1. **Vérifier le lancement local**
   ``
   php bin/serve
   ``

2. **Installer les dépendances**
   ``
   composer install --optimize-autoloader
   ``

3. **Vérifier le fichier README.md**

4. **Configurer la base de données**
   - Vérifier les informations dans le fichier `.env` :
     - `DB_USER`
     - `DB_PASSWORD` 
     - `DB_HOST`
     - `DB_NAME`

### Problème SSH (si nécessaire)

Si erreur de fingerprint lors de la connexion SSH :
- Aller dans le fichier `known_hosts` (généralement à la racine du dossier utilisateur)
- Supprimer la ligne contenant l'IP du serveur

## 2. Installation et configuration d'aaPanel

### Installation d'aaPanel sur le VPS

``
URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel
``

### Configuration d'aaPanel

1. Se connecter avec les identifiants fournis
2. Choisir serveur **LNMP (nginx)**
3. Cliquer sur "one click"
4. Laisser l'installation se faire

### Paramétrage pour le déploiement

1. Cliquer sur "Add site"
2. Mettre l'IP de la machine dans le nom de domaine
3. Description : nom du projet (ex: habit-tracker-buggy-web-app-bloc-4-dfs-2025-bis-mela57)
4. Renommer le dossier avec le nom de la description
5. Base de données : **MySQL**
6. Décocher "create html file"
7. Cliquer sur "confirm"
8. **Conserver les informations fournies**

## 3. Configuration Git et déploiement

### Création du dépôt distant (sur le VPS)

``
cd /var
mkdir depot-git  
cd depot-git
git init --bare
``

### Ajout du remote (en local)

``
git remote add vps root@ip_de_la_vm:/var/depot_git
``

### Premier push

``
git push -u vps master
# ou
git push vps
``

## 4. Déploiement du code

### Déploiement manuel

``
git --git-dir=/var/depot_git --work-tree=/www/wwwroot/nom_du_site checkout -f {tag_ou_branche}
``

### Configuration finale

1. **Dans aaPanel :**
   - Aller dans "Website"
   - Cliquer sur l'IP du site
   - Pointer vers le dossier **public** dans "Site Directory"
   - Lancer composer

2. **Configuration de l'environnement :**
   - Créer le fichier `.env` avec les paramètres de production
   - Aller dans "Database", créer une base de données
   - Copier les informations de connexion dans le `.env`

## 5. Automatisation du déploiement

### Création du script de déploiement

``
touch deploy.sh
nano deploy.sh
``

**Contenu du script :**
``
VARNAME=${1:?"missing arg 1 for tag name or branch name"}
git --git-dir=/var/depot_git --work-tree=/www/wwwroot/bloc4-dfs-training checkout -f $VARNAME
``

### Rendre le script exécutable

``
chmod +x deploy.sh
``

### Utilisation du script

``
./deploy.sh master
# ou
./deploy.sh nom_du_tag
``

## 6. Gestion des versions avec Git Cliff

### Installation de git-cliff

``
wget "https://github.com/orhun/git-cliff/releases/download/v2.9.1/git-cliff-2.9.1-x86_64-unknown-linux-gnu.tar.gz"
tar -xzf git-cliff-2.9.1-x86_64-unknown-linux-gnu.tar.gz
sudo mv git-cliff-2.9.1/git-cliff /usr/local/bin/
sudo chmod +x /usr/local/bin/git-cliff
rm -rf git-cliff-2.9.1*
``

### Configuration de git-cliff

**Initialisation (à la racine du projet) :**
``
git cliff --init
``

**Génération du changelog :**
``
git cliff -o CHANGELOG.md
``

**Génération avec auto-versioning :**
``
git cliff --bump -o CHANGELOG.md
``

**Imposer une version majeure :**
``
git cliff --tag 1.0.0 -o CHANGELOG.md
``

### Conventions de versioning

**Format : V.X.X.X**
- **Premier X** : version majeure (déploiement, gros changements)
- **Deuxième X** : version mineure (nouvelles fonctionnalités)
- **Troisième X** : patch (correction de bugs)

### Workflow des commits

1. Faire des commits avec les conventions : `feat`, `fix`, `docs`, etc.
2. Utiliser `git cliff --bump -o CHANGELOG.md` après chaque commit
3. Faire `git commit -a -m "commit message"`

**Important pour le commit du CHANGELOG :**
- Commiter le CHANGELOG seul
- Ne pas utiliser de commit conventionnel
- Message : "version X.X.X"

### Gestion des tags
``
git push vps tag 1.0.0
``

## Notes importantes

- Le fichier `cliff.toml` peut être modifié pour ajouter ou personnaliser les types de commits conventionnels
- Possibilité d'ajouter des gitmojis ou autres noms personnalisés
- Git cliff calcule automatiquement les tags avec la commande `--bump`

