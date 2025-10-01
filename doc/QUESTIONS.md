# Questions

Répondez ici aux questions théoriques en détaillant un maxium vos réponses :

1) Expliquer la procédure pour réserver un nom de domaine chez OVH avec des captures d'écran (arrêtez-vous au paiement) :
Il fuat deja se crer un compte, ensuite il faut verifié que le nom de domaine qu'on souhaite est disponible. Une fois qu"on a choisir son type d'abonnement et son nom de domaine ( qui est gratuit la première année), o passe au paiement.

2. Comment faire pour qu'un nom de domaine pointe vers une adresse IP spécifique ?
Lier un domaine à une adresse IP est une étape fondamentale dans la création d’un site web. Ce processus implique de configurer les paramètres DNS (Domain Name System) du nom de domaine pour qu’il pointe vers le serveur où est hébergé le site web. 

3. Comment mettre en place un certificat SSL ?
Un certificat SSL (Secure Sockets Layer) est essentiel pour sécuriser la communication entre un site web et ses utilisateurs en cryptant les données transmises sur l’internet. Il contribue à instaurer la confiance en garantissant la protection des informations sensibles, telles que les identifiants de connexion, les détails de paiement et les données personnelles. Les certificats SSL sont également un facteur clé pour le référencement, car les moteurs de recherche comme Google donnent la priorité aux sites web dotés du protocole HTTPS par rapport au protocole HTTP.

exemple avec SSH manuellement avec Nginx

Téléchargez les fichiers du certificat sur le serveur: Utilisez un client SFTP comme FileZilla ou la commande scp pour télécharger les fichiers certificate.crt, private.key et ca_bundle.crt sur votre serveur.


Pour Nginx:
sudo nano /etc/nginx/sites-available/votredomaine.com


server {
listen 443 ssl ;
server_name votredomaine.com ;
ssl_certificate /path/to/certificate.crt ;
ssl_certificate_key /path/to/private.key ;
ssl_trusted_certificate /path/to/ca_bundle.crt ;
}

sudo systemctl restart nginx
pour verifier l'installation:  https://yourdomain.com dans le navigateur pour vérifier que le certificat SSL est correctement installé.
