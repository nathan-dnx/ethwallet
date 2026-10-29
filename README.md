# Ethereum Home Node Deployment

## 1. Project Overview
Déploiement d'un nœud Ethereum complet (Exécution + Consensus) synchronisé sur le mainnet depuis un VPS, avec compilation depuis les sources.

## 2. Client Selection
*   **Execution Client : Geth.** Choisi pour sa robustesse, sa forte adoption sur le réseau et sa compatibilité éprouvée.
*   **Consensus Client : Lighthouse.** Choisi pour ses performances en Rust, sa légèreté relative et sa fonction de `checkpoint-sync` permettant une synchronisation rapide.

## 3. System Requirements & Storage Configuration
*   **Contrainte matérielle rencontrée :** Le VPS fourni ne disposait que d'un disque additionnel de 1 To (`/dev/sdb`), inférieur aux 2 To exigés. 
*   **Solution :** Formatage en `ext4` et montage du disque sur le répertoire `/data` pour y héberger les sources et la base de données. Configuration d'un montage persistant via `/etc/fstab` pour garantir le redémarrage automatique.

## 4. Step-by-Step Installation Guide
*(Décris brièvement les commandes utilisées pour installer Go, Rust, et les `make geth` / `make` pour compiler les clients).*

## 5. Service Configuration & Auto-start
*(Explique la création des fichiers systemd et le test de reboot).*

## 6. RPC Endpoint Security
*(Explique que le point d'accès HTTP est exposé sur le port 8545 avec les namespaces `eth` et `web3` activés).*

## 7. Troubleshooting
*   **Erreur d'espace disque :** Le disque principal (`/dev/sda1`) était plein à 100%. Résolu en libérant de l'espace et en déplaçant toute l'installation sur `/data`.
*   **Erreur 203/EXEC au redémarrage :** Le montage de `/data` n'était pas persistant, rendant les binaires inaccessibles après le boot. Résolu en éditant `/etc/fstab`.
*   **Erreur cURL (7) sur localhost :** Geth écoutant sur l'IPv4 (`0.0.0.0`), la requête locale a dû être forcée sur `127.0.0.1` au lieu de `localhost` (IPv6 par défaut).
