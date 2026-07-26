# Administration système - Stratos Datacenter

Petit récap des commandes utilisées pour gérer users et groupes sur l'infra Nautilus (App servers stapp01/02/03, via le jump host).

## Détails de l'infrastructure

| Serveur | IP | Hostname | User | Mot de passe | Rôle |
|---|---|---|---|---|---|
| Application Server 1 | Dynamique | stapp01 | tony | Ir0nM@n | Héberge Nautilus Application 1 |
| Application Server 2 | Dynamique | stapp02 | steve | Am3ric@ | Héberge Nautilus Application 2 |
| Application Server 3 | Dynamique | stapp03 | banner | BigGr33n | Héberge Nautilus Application 3 |
| LoadBalancer Server | Dynamique | stlb01 | loki | Mischi3f | Répartit le trafic HTTP pour Nautilus |
| Database Server | Dynamique | stdb01 | peter | Sp!dy | Héberge la base de données Nautilus |
| Storage Server | Dynamique | ststor01 | natasha | Bl@kW | Stocke les données des serveurs Nautilus |
| Backup Server | Dynamique | stbkp01 | clint | H@wk3y3 | Gère les sauvegardes des serveurs Nautilus |
| Mail Server | Dynamique | stmail01 | groot | Gr00T123 | Gère les services email de Nautilus |
| Jump Host Server | Dynamique | jump-host | thor | mjolnir123 | Accès sécurisé au datacenter Stork |
| Jenkins Server | Dynamique | jenkins | jenkins | j@rv!s | Fait tourner Jenkins pour le pipeline CI/CD |

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
