## Linux : connexion SSH et création d'utilisateur

Connexion au serveur `stapp01` avec le compte `tony` :

```bash
ssh tony@stapp01
```

Première connexion, donc il faut valider l'empreinte de la clé ED25519 du serveur avant de rentrer le mot de passe.

Ensuite il fallait créer un utilisateur `mariyam` avec un UID fixe (1274) et un home directory qui sort de l'ordinaire — `/var/www/mariyam` au lieu de `/home/mariyam` :

```bash
sudo useradd -m -u 1274 -d /var/www/mariyam mariyam
```

`-m` pour créer le home s'il existe pas, `-u 1274` pour l'UID, `-d` pour changer l'emplacement.

Mot de passe :
```bash
sudo passwd mariyam
```

Vérif rapide :
```bash
id mariyam
```
`uid=1274(mariyam) gid=1274(mariyam) groups=1274(mariyam)` — bon, l'UID est le bon.

```bash
grep mariyam /etc/passwd
```
confirme que l'entrée est bien dans le fichier système.

**Résumé :** SSH + sudo + useradd avec UID et home custom, et vérification avec id/etc.passwd.
