# Sécurité LehanEOS

**Document** : SECURITY
**Version** : 1.0
**Auteur** : Yohan Grondin
**Dernière mise à jour** : 2026-09-24

---

## 1. Objectif

Ce document décrit les principes de sécurité appliqués à LehanEOS.

LehanEOS est conçu selon le principe du moindre privilège et de la séparation des responsabilités.

Les mécanismes de sécurité seront déployés progressivement au rythme de l'évolution de la plateforme.

> LehaneOS n'a pas vocation à obtenir des privilèges élevés. Les actions sont réalisées au travers de comptes délégués disposant uniquement des autorisations strictement nécessaires.

---

## Principes fondamentaux

### Moindre privilège

Les comptes de service ne doivent disposer que des droits strictement nécessaires à l'exécution des tâches demandées.

### Séparation des responsabilités

Les rôles RH, IAM, administration système et exploitation doivent rester clairement séparés.

### Source de vérité unique

Les informations RH doivent être saisies une seule fois puis propagées vers les systèmes concernés.

### Auditabilité

Toute action critique doit être traçable et journalisée.

## Sécurité V1

Objectif : sécuriser le socle de la plateforme.

Mesures prévues :

- Compte de service dédié
- Délégations Active Directory minimales
- Aucun compte Domain Admin utilisé par l'application
- Journalisation des actions
- Gestion centralisée de la configuration
- Secrets stockés hors du code source

## Gestion des secrets

Les informations sensibles ne doivent jamais être enregistrées dans le dépôt Git.

Exemples :

- mots de passe
- clés API
- secrets JWT
- chaînes de connexion

Ces informations doivent être stockées dans :

- .env
- variables d'environnement
- coffre-fort de secrets (évolution future)

## Active Directory

Le compte utilisé par LehaneOS doit être un compte dédié.

Exemple :

svc_lehaneos_runner

Le compte ne doit pas :

- être Domain Admin
- être administrateur local
- disposer d'accès interactifs inutiles

Les privilèges doivent être accordés par délégation sur les objets concernés.

## Évolutions futures

### Scripts signés

- PKI interne
- Certificats Code Signing
- Validation de la signature des scripts

### PowerShell

- ExecutionPolicy AllSigned
- Contrôle des scripts approuvés

### Bastion

- Point d'administration unique
- Restriction des accès directs aux serveurs

### Accès JIT

- Attribution temporaire de privilèges
- Expiration automatique des accès

### PAM

- Gestion des comptes privilégiés
- Audits renforcés

## Hors périmètre actuel

Les éléments suivants sont identifiés mais ne font pas partie des versions initiales :

- Bastion d'administration
- PAM
- Rotation automatique des secrets
- PKI complète
- Gestion des certificats
- Gouvernance avancée des accès