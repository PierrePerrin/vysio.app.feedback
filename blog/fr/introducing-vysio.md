---
title: "Coder sur iPad : exécuter VS Code et GitHub Codespaces dans un client natif"
date: "2026-06-21"
description: "Pourquoi Safari complique l'usage de Codespaces sur iPad, et ce que Vysio change pour les raccourcis, la veille et les identifiants GitHub."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "4 min de lecture"
---

J'ai longtemps essayé d'utiliser l'iPad comme vraie machine de développement. Le matériel n'était pas le problème : une puce Apple Silicon, un bel écran, un Magic Keyboard et une bonne connexion suffisent largement quand le calcul tourne ailleurs.

Avec GitHub Codespaces, Gitpod ou une instance `code-server`, tout devrait donc être simple. L'éditeur se charge bien. Puis les petits problèmes de navigateur commencent à s'accumuler.

C'est précisément là que **Vysio** intervient.

## Là où Safari bloque

Vous pouvez ouvrir `github.dev` ou l'URL de votre `code-server` dans Safari et retrouver une interface VS Code familière. Le sujet n'est pas le chargement de l'éditeur. Le sujet, c'est ce qui se passe quand vous commencez vraiment à travailler.

### 1. Conflits de raccourcis clavier
Le premier problème, ce sont les réflexes. Vous appuyez sur `Cmd + W` pour fermer un onglet dans VS Code, et Safari ferme l'onglet du navigateur. Vous appuyez sur `Cmd + P` pour ouvrir le sélecteur de fichiers, et Safari affiche la fenêtre d'impression.

Ce ne sont pas des raccourcis secondaires. Ce sont ceux qu'on utilise toute la journée.

### 2. Veille et déconnexions intempestives
Les environnements cloud ont besoin d'une connexion stable. Si l'écran de l'iPad se met en veille pendant une compilation ou une suite de tests, Safari peut perdre la connexion WebSocket. Au réveil, vous attendez la reconnexion au lieu de lire le résultat.

### 3. Stockage des identifiants
Pour piloter vos Codespaces proprement, une application doit conserver des identifiants OAuth GitHub. Le stockage navigateur n'est pas le meilleur endroit pour ça, et il peut être vidé dans certains cas par iOS. Résultat : vous repassez par une connexion GitHub au moment où vous vouliez juste ouvrir votre projet.

---

## Ce que Vysio fait autrement

Vysio est une application iPad native construite autour d'une vue WebKit configurée pour ce cas d'usage. L'objectif est volontairement précis : rendre VS Code distant et Codespaces utilisables sur iPad, sans ajouter de serveur entre votre appareil et GitHub.

### Raccourcis transmis à l'éditeur
Vysio configure sa couche WebKit pour que les raccourcis courants arrivent dans l'espace de travail distant. `Cmd + W`, `Cmd + N`, `Cmd + T` et `Cmd + P` sont transmis à VS Code au lieu d'être traités comme des commandes de navigateur.

### Verrouillage de la mise en veille
Lorsque vous travaillez dans un espace, Vysio empêche l'iPad de se mettre en veille. Vos compilations longues se terminent sans interruption et vos connexions sockets restent stables.

### Identifiants dans le Trousseau Apple
Vos jetons GitHub sont stockés dans le Trousseau d'accès Apple, protégés par Face ID, Touch ID ou le code de l'iPad. Vysio communique directement avec les API de GitHub depuis votre appareil, sans serveur Vysio au milieu.

### Plus de place pour l'éditeur
Sans barre d'adresse, onglets de navigateur ni commandes de navigation, l'éditeur récupère beaucoup plus d'espace. Avec Stage Manager ou un écran externe, l'ensemble se rapproche d'un vrai poste de travail concentré.

---

## Essayer Vysio

Vysio est actuellement disponible en bêta privée TestFlight. Si vous voulez essayer Codespaces sur iPad sans vous battre avec les raccourcis de Safari, inscrivez-vous sur la page d'accueil et je vous enverrai une invitation lors des prochaines ouvertures.
