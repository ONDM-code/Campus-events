#  Uni Events

[![Database: Supabase](https://img.shields.io/badge/Backend-Supabase-green?style=flat-square&logo=supabase)](https://supabase.com/)
[![Database: PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blue?style=flat-square&logo=postgresql)](https://www.postgresql.org/)
[![Security: 2FA](https://img.shields.io/badge/Security-2FA_Enabled-red?style=flat-square)](#)

**Uni Events** est une application web centralisée conçue pour dynamiser et organiser la vie étudiante sur le campus. La plateforme permet de publier, planifier, consulter et gérer l'ensemble des activités et événements universitaires à travers une interface fluide et sécurisée.

---

##  Objectifs du Projet

* **Centralisation :** Regrouper l'agenda de tous les événements du campus sur une plateforme unique.
* **Expérience Utilisateur :** Offrir une interface moderne, intuitive et accessible pour les étudiants.
* **Sécurité Native :** Garantir la protection des comptes et l'isolation des données grâce à **Supabase Auth**.
* **Authentification Forte :** Intégrer une vérification à deux facteurs (2FA) pour sécuriser les accès sensibles.

---

##  Fonctionnalités Clés

### Authentification & Sécurité
* Création de compte utilisateur et connexion sécurisée.
* Module de réinitialisation de mot de passe.
* Activation et gestion de la double authentification (2FA).

###  Gestion des Événements
* Création et publication d'événements avec formulaires contrôlés.
* Consultation de la liste globale des événements via un agenda dynamique.
* Page de détails dédiée pour chaque activité (lieu, date, heure, description).

###  Interaction & Suivi
* Système d'inscription et gestion des listes de participants par événement.
* Notifications automatisées en temps réel pour informer les utilisateurs.

---

##  Modélisation de la Base de Données

Le projet s'appuie sur une modélisation relationnelle stricte afin d'éviter les redondances de données et de garantir une intégrité référentielle totale.

###  Modèle Conceptuel des Données (MCD)
* **UTILISATEUR :** `id_utilisateur`, prénom, nom, email, rôle, date_creation.
* **ÉVÉNEMENT :** `id_evenement`, titre, description, date, heure, lieu, statut.
* **CATÉGORIE :** `id_categorie`, nom_categorie.
* **INSCRIPTION :** `id_inscription`, date_inscription, statut.
* **NOTIFICATION :** `id_notification`, message, date_envoi, lu.
* **SÉCURITÉ :** `id_securite`, secret_totp, actif.

###  Modèle Relationnel (MLD)
```text
UTILISATEUR(id_utilisateur PK, prenom, nom, email UNIQUE, role, date_creation)
CATEGORIE(id_categorie PK, nom_categorie)
EVENEMENT(id_evenement PK, titre, description, date_evenement, lieu, statut, id_createur FK, id_categorie FK)
INSCRIPTION(id_inscription PK, date_inscription, statut, id_utilisateur FK, id_evenement FK)
NOTIFICATION(id_notification PK, message, date_envoi, lu, id_utilisateur FK)
SECURITE(id_securite PK, secret_totp, actif, id_utilisateur FK UNIQUE)
