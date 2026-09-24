# Architecture LehanEOS
**Version** : 1.0 
**Auteur** : Yohan Grondin
**Dernière mise à jour** : 2026-09-24

---

## Vision

LehaneOS est une plateforme modulaire d'orchestration d'entreprise.

L'objectif est de fournir un socle permettant d'intégrer progressivement
plusieurs domaines métiers :

- Ressources Humaines (RH)
- Identity & Access Management (IAM)
- Self-Service Application Portal (SSAP)
- Gestion des actifs
- Intégrations externes

LehaneOS n'a pas vocation à remplacer les solutions existantes
(Active Directory, GLPI, ERP, CRM, etc.) mais à les orchestrer au travers
d'une expérience utilisateur unique.

---

## Principes d'architecture

### Architecture modulaire

Le projet adopte une architecture orientée domaine (Domain Based Architecture).

Chaque domaine métier possède son propre espace :

- **rh/**
- **iam/**
- **ssap/**
- **assets/**

Chaque module est responsable de son API, de ses services,
de ses modèles et de ses repositories.

Cette approche facilite :

- la maintenance
- les évolutions futures
- la séparation des responsabilités
- l'ajout de nouveaux modules

### Pourquoi une architecture par domaine ?

Deux approches ont été étudiées :

#### Architecture par couches
```text
api/
services/
repositories/
models/
```

Cette approche est adaptée aux applications simples reposant
sur un périmètre métier unique.

#### Architecture par domaine
```text
rh/
iam/
assets/
```

Cette approche est privilégiée dans LehaneOS car le projet a
vocation à accueillir plusieurs domaines métiers indépendants.

Chaque module reste autonome et peut évoluer sans impact
important sur les autres modules.

---

## Structure du projet
```text
LehanEOS/
│
├── docs/
│   ├── roadmap.md
│   ├── conventions.md
│   ├── architecture.md
│   ├── security.md
│   └── active-directory.md
│
├── src/
│   └── lehaneos/
│       ├── core/
|       |   ├── exceptions/
|       |   |   └── exceptions.py
|       |   ├── middlewares/
|       |   ├── security/
│       │   ├── logging.py
│       │   └── powershell_runner.py
│       ├── settings/
│       │   └── config.py
│       ├── database/
|       ├── cli/
│       ├── iam/    
│       |    ├── api/
│       |    ├── services/
│       |    ├── repositories/
│       |    ├── schemas/
│       |    └── models/
│       ├── rh/    
│       │    ├── api/
│       |    ├── services/
│       |    ├── repositories/
│       |    ├── schemas/
│       |    └── models/
|       ├── integrations/
|       |    ├── active_directory/
|       |    ├── glpi/
|       |    ├── mqtt/
|       |    └── service_now/
|       ├── utils/
|       |
│       └── main.py
│
├── tests/
│
├── scripts/
│   ├── powershell/
│   └── sql/
|
├── .env
├── .env.example
├── pyproject.toml
└── README.md
```

---

## Évolution prévue

Les modules suivants sont actuellement envisagés :

### V1

- RH
- IAM

### V2

- Assets
- Intégrations GLPI

### V3

- SSAP

### V4

- ERP
- CRM

### V5

- Reporting
- Gouvernance

---

## Règles d'architecture

- Le code métier ne doit pas dépendre directement d'une intégration externe.
- Les échanges avec Active Directory passent par le module integrations.
- Les échanges avec GLPI passent par le module integrations.
- Les modules métier doivent rester indépendants.
- Les services ne doivent pas accéder directement à la base de données.
- Les accès aux données passent par les repositories.
