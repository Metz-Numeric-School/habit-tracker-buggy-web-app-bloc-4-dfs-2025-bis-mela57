# TODO

Suite à un audit effectué en amont, voici les failles et les bugs qui ont été identifés comme prioritaire.

## FAILLES

* Des utilsateurs non admin ont des accès à l'interface de gestion des utilisateurs
* Les mots de passes ne sont pas chiffrée en base de données...
* Des injections de type XSS ont été détéctées sur certains formulaires
* On nous a signalé des injections SQL lors de la création d'une nouvelles habitudes
  * exemple dans le champs "name" : foo', 'INJECTED-DESC', NOW()); --

## BUGS

* Une 404 est détéctée lors de l'accès à l'URL ``/habit/toggle``
* Fatal error: Uncaught Error: Class "App\Controller\Api\HabitsController" lorsque l'on accède à l'URL  ``/api/habits``

**ATTENTION : certains bugs n'ont pas été listé**

Beaucoup d'entrées n'ont pas de htmlspecialchars ce qui cause des failles XSS
Les mots de passes n'ont pas de passwordhash, donc si jamais la base de données est hackée, tous les mots de passe sont en clairs
Toutes les requetes ne sont pas préparées, il aurait fallu inclure soit bindParam soit l'attribut prepare()
Dans le securityController on retrouve un die ce qui fait que le code qui suit n'est pas exécuté, ce qui explique pourquoi des utilisateur non admin ont accès a l'interface de gestion des utilisateurs.
