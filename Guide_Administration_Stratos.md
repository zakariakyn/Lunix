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


