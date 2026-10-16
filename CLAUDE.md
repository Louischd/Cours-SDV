# Cours SDV — instructions pour la génération automatique

Ce repo est un site Quartz v5. Les cours sont dans `content/`. Tout est rédigé **en français**.
Le site est **public** : aucune information interne d'entreprise (noms de serveurs, clients, IP, architecture interne), aucun secret.

## Procédure quotidienne (tâche de 18h)

1. `git pull` sur `main`.
2. Lire `content/inbox.md`, section **« À traiter »**. Si elle est vide : ne rien modifier, ne rien committer, terminer.
3. Pour chaque ligne (`- MOT-CLÉ` ou `- MOT-CLÉ - contexte`) :
   1. Chercher si un cours existe déjà sur le sujet (nom de fichier, `title`, `aliases`) dans `content/`. S'il existe, **compléter** ce cours (en tenant compte du contexte) au lieu d'en créer un doublon.
   2. Choisir la catégorie : `reseau`, `securite` ou `systemes`. Si aucune ne convient vraiment, créer un nouveau dossier en minuscules sans accents avec son `index.md` (frontmatter `title` accentué + `description`), et l'ajouter à la liste de `content/index.md`.
   3. Rédiger le cours selon le **modèle** ci-dessous, dans `content/<categorie>/<Nom>.md`. Nom de fichier = nom usuel de la notion (ex. `IPsec.md`, `Diffie-Hellman.md`), sans `/` ni `:`.
   4. Ajouter le cours dans la liste `## Cours` du `index.md` de sa catégorie (une ligne : `- [[Nom]] : résumé en une phrase`), ordre alphabétique.
   5. Ajouter des liens `[[...]]` vers les cours existants pertinents, et dans les cours existants fortement liés, ajouter un lien retour dans leur section « Notions liées ».
   6. Déplacer la ligne de « À traiter » vers « Traité » sous la forme `- [[Nom]] — AAAA-MM-JJ`.
   7. Ajouter dans « Suggéré » les notions liées citées en `[[...]]` qui n'ont pas encore de cours et qui ne sont pas déjà listées (pas de doublon, maximum 5 par cours).
4. Vérifier le build : `npm ci` si `node_modules` absent, puis `npx quartz build`. Le build doit réussir.
5. Committer avec le message `cours: <mots-clés traités>` et pousser sur `main`.

Ne jamais supprimer un cours existant. Ne pas toucher à la configuration Quartz ni aux workflows.

## Qualité attendue

- Langage simple d'abord (expliquer comme à un collègue), puis le détail technique. Pas de définition de manuel en ouverture.
- Exact et vérifiable : en cas de doute sur un détail, ne pas l'inventer. Citer les références normatives (RFC, docs éditeur) dans « Pour aller plus loin ».
- Concret : commandes et configurations réelles, pour Linux et Windows quand c'est pertinent.
- Longueur visée : 800 à 1 500 mots.

## Modèle de cours

```markdown
---
title: <Nom>
description: <résumé en une phrase>
categorie: <reseau|securite|systemes>
tags:
  - <tag1>
  - <tag2>
aliases:
  - <autre nom éventuel>
niveau: <débutant|intermédiaire|avancé>
date: AAAA-MM-JJ
---

## En bref

3 à 5 lignes : à quoi ça sert, en langage simple, avec une analogie si elle aide.

## Pourquoi ça existe

Le problème que la notion résout.

## Comment ça marche

Explication détaillée, étape par étape. Schéma Mermaid si un flux s'y prête.

## En pratique

Commandes / configuration concrètes, avec commentaires.

## Pièges courants

Liste des erreurs fréquentes et comment les diagnostiquer.

## Notions liées

- [[Notion A]] : lien avec ce cours en une phrase

## Quiz

> [!question]- 1. Question ?
> Réponse et explication.

(5 questions, en callouts repliables comme ci-dessus)

## Pour aller plus loin

- RFC / documentation officielle
```
