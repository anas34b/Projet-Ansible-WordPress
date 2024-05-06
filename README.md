# Projet Ansible WordPress

## Auteur

DAOUI Anas

## Description

Ce projet automatise le déploiement d'un site WordPress sur deux instances, en utilisant Ansible pour configurer Nginx, PHP, MySQL, et pour cloner WordPress. Une vérification de la connexion à la base de données et le déploiement d'WordPress sont inclus.

## Instances

- **v1** - 192.168.140.39
- **v2** - 192.168.140.34

## Prérequis

- Docker et Docker Compose (pour l'environnement de test local)
- Accès SSH aux serveurs cibles
- VPN de l'IUT pour accéder aux instances

## Configuration Initiale

1. **Cloner le Projet** : Clonez le dépôt du projet depuis le lien du Git.
2. **Lancer Docker** (optionnel) : Si vous utilisez un environnement de test local.
3. **Configurer l'Accès SSH ou l'utilisation de vos propres instances** :
   - Si vous avez des instances basés sur débiane, vous n'avez cas remplacer mes adresses ip dans le inventory.ini par les votres.
   - Sinon, Utilisez la clé SSH nommée `prof`, disponible dans le mail envoyé. Les fichiers nécessaires ont été ajoutés sur OpenStack.
   - Exécutez les commandes suivantes pour configurer l'agent SSH :
     ```
     eval $(ssh-agent -s)
     ssh-add ~/.ssh/id_rsa
     ssh-add -l
     ```
   - Assurez-vous d'activer le VPN de l'IUT pour accéder aux instances.
   - Testez la connexion SSH avec : `ssh debian@<adresse_ip>`
   
4. **Installer les Collections Ansible Nécessaires** :
```
ansible-galaxy collection install community.mysql
```

## Déploiement

Dans le dossier cloné, exécutez :
```
make sh # Exécutez les scripts nécessaires avant le déploiement
```


Ensuite, lancez le playbook Ansible avec :
```
ansible-playbook -i inventory.ini site.yml
```


## Vérification

Après le déploiement ou avant, vous pouvez voir le fonctionnement :

- **Connexion à la Base de Données** : Accédez à `http://192.168.140.39/connection_test.php`. Vous devriez voir "Connexion réussie".
- **WordPress** : Accédez à `http://192.168.140.39/wordpress` pour voir la page d'accueil de WordPress.

## Environnements

Le projet est configuré pour fonctionner sur deux machines :

- **v1** (Staging)
- **v2** (Production)

Assurez-vous d'avoir configuré correctement vos environnements et suivi toutes les étapes nécessaires pour un déploiement réussi.

