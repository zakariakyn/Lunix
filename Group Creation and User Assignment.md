# Group Creation and User Assignment

Petit récap des commandes utilisées pour gérer users et groupes sur l'infra Nautilus (App servers stapp01/02/03, via le jump host).

## Connexion aux serveurs

Chaque serveur se gère séparément, en SSH depuis le jump host :

- App Server 1 : `ssh tony@stapp01`
- App Server 2 : `ssh steve@stapp02`
- App Server 3 : `ssh banner@stapp03`

## Créer un groupe

```bash
sudo groupadd <nom_du_groupe>
```

Exemple : `sudo groupadd nautilus_admin_users`

## Gérer les utilisateurs

**Utilisateur pas encore créé** — on le crée directement avec le bon groupe secondaire via `-G` :

```bash
sudo useradd -G <nom_du_groupe> <nom_utilisateur>
```

Exemple : `sudo useradd -G nautilus_developers jarod`

Attention, `-a` n'existe pas pour `useradd` (piège classique) — cette option est réservée à `usermod`.

**Utilisateur déjà existant** — on l'ajoute au groupe avec `usermod -aG` (append, sans écraser ses groupes actuels) :

```bash
sudo usermod -aG <nom_du_groupe> <nom_utilisateur>
```

Exemple : `sudo usermod -aG nautilus_developers jarod`

## Vérifier que ça a marché

`getent` est la commande la plus fiable pour checker un groupe et voir qui en fait partie :

```bash
getent group <nom_du_groupe>
```

Sinon on peut aussi juste chercher dans `/etc/group` :

```bash
grep <nom_du_groupe> /etc/group
```

Si tout est bon, la ligne renvoyée ressemble à `nom_du_groupe:x:GID:utilisateurs` — par exemple `nautilus_developers:x:1001:jarod`. Si le groupe est vide, la partie utilisateurs après le dernier `:` sera juste vide.
