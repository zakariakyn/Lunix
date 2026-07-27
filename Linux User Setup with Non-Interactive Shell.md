# Création d'un utilisateur avec shell non-interactif

Tâche : créer un utilisateur `james` avec un shell non-interactif sur App Server 3 (`stapp03`), pour l'outil d'agent de backup.

## Connexion au serveur

```bash
ssh banner@stapp03
```

## Création de l'utilisateur

```bash
sudo useradd -s /sbin/nologin james
```

`-s /sbin/nologin` fixe le shell de connexion à `nologin`, donc l'utilisateur ne peut pas ouvrir de session interactive — exactement ce qu'il faut pour un compte de service comme un agent de backup.

⚠️ Piège rencontré : la première tentative a créé `ravi` au lieu de `james` (probablement copié-collé d'un exercice précédent). Si ça arrive, il suffit de relancer la commande avec le bon nom, et éventuellement supprimer le mauvais utilisateur si besoin :

```bash
sudo userdel ravi
```

## Vérification

Vérifier que l'utilisateur existe avec le bon UID/GID :

```bash
id james
```

Vérifier spécifiquement le shell configuré :

```bash
getent passwd james
```

Le dernier champ de la ligne retournée doit afficher `/sbin/nologin`, ce qui confirme que le shell non-interactif est bien en place.
