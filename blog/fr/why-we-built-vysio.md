---
title: "Pourquoi nous avons créé Vysio : l'expérience développeur sur iPad méritait mieux"
date: "2026-06-14"
description: "L'histoire derrière Vysio : pourquoi coder sur iPad fonctionnait presque, où le navigateur bloquait, et pourquoi nous avons construit un client natif."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "5 min de lecture"
---

Il existe une frustration bien particulière que seuls les développeurs connaissent : quand le bon outil existe presque.

Depuis deux ans, j'essaie de faire de mon iPad mon principal outil de développement. Pas parce que c'est à la mode. Parce qu'un iPad Pro avec une puce M4, une connexion cellulaire et un Magic Keyboard est sincèrement le meilleur ordinateur portable que j'aie jamais eu. Il est léger, silencieux, son écran est excellent et sa batterie tient toute la journée.

Le matériel était prêt. Le logiciel ne l'était pas.

## La configuration qui aurait dû fonctionner

GitHub Codespaces aurait dû régler le problème. La puissance de l'environnement de développement n'était plus liée à l'appareil entre vos mains. Une instance VS Code dans le cloud, un accès terminal complet, du stockage persistant — tout cela accessible depuis n'importe quel navigateur, sur n'importe quel appareil.

"N'importe quel appareil" — y compris l'iPad.

J'ai donc essayé. J'ai ouvert `github.dev` dans Safari. Ça a chargé. Ça avait l'air bien. Et puis j'ai commencé à vraiment écrire du code.

En cinq minutes, j'avais :
- Déclenché une boîte de dialogue d'impression Safari en essayant d'ouvrir un fichier avec `Cmd + P`
- Fermé accidentellement mon onglet de navigation en essayant de fermer un onglet d'éditeur avec `Cmd + W`
- Perdu ma connexion Codespace alors que l'écran iPad s'était mis en veille pendant une compilation longue

Le troisième problème était le plus décourageant. La compilation était presque terminée. J'ai regardé ailleurs pendant trente secondes. Quand je suis revenu, la connexion WebSocket était morte et j'ai dû relancer la compilation.

## Ce qu'on a essayé en premier

La première étape évidente était de chercher une application existante. Quelque chose conçu spécifiquement pour coder dans Codespaces depuis l'iPad.

Il n'y avait rien. Pas vraiment.

Il y avait des clients SSH, qui résolvent un problème différent. Il y avait des éditeurs généralistes. Il y avait des expériences et des raccourcis partagés sur Reddit. Je n'ai pas trouvé d'outil qui traite l'iPad comme un vrai client pour les outils que j'utilisais déjà : Codespaces, VS Code, les raccourcis clavier matériels et l'authentification GitHub sécurisée.

On l'a donc construit.

## Les décisions qui ont façonné Vysio

**Aucun backend. Jamais.**

La première décision de conception était la plus importante : Vysio ne toucherait jamais vos jetons GitHub sur un serveur que nous contrôlons. Votre jeton OAuth vit dans le Trousseau Apple sur votre appareil, protégé par Face ID. Les connexions à l'API GitHub sont établies directement depuis votre iPad. Nous n'avons aucun serveur qui pourrait être compromis, aucune base de données qui pourrait exposer vos identifiants.

Ce n'était pas une fonctionnalité. C'était une contrainte que nous nous sommes imposée avant d'écrire la moindre ligne de code.

**WKWebView configuré pour les développeurs, pas pour les consommateurs.**

La deuxième décision était technique. Nous ne voulions pas d'une simple enveloppe qui ouvre une URL. Nous avons configuré une couche `WKWebView` pour que les raccourcis de l'éditeur atteignent le contenu web au lieu d'être avalés par des commandes de navigateur. `Cmd + W`, `Cmd + P`, `Cmd + T`, `Cmd + N` — tous passent à l'éditeur.

**Écran actif, connexion maintenue.**

Nous avons implémenté un verrou de veille pour que Vysio maintienne l'affichage de votre iPad allumé quand un espace de travail est ouvert. Les compilations longues et les suites de tests ne dépendent plus d'un tapotement régulier sur l'écran.

**Tableau de bord natif, pas un onglet de navigateur.**

L'expérience de gestion des Codespaces — lister vos espaces de travail, voir leur état, les démarrer et les arrêter — se passe dans une interface SwiftUI native. Vous voyez vos Codespaces dès l'ouverture de l'application, avec leur statut actuel, avant même d'ouvrir un éditeur.

## Ce que Vysio n'est pas

On nous demande souvent : "Est-ce que Vysio peut faire tourner un code-server local ?" ou "A-t-il un terminal intégré ?" La réponse est non, et c'est intentionnel.

Vysio est un client natif pour les environnements de développement distants. Le calcul se passe dans le cloud. Vysio est la fenêtre par laquelle vous y accédez, et il rend cette fenêtre aussi propre et fiable que possible sur iPad.

Nous n'essayons pas de reproduire un Mac. Nous essayons de faire fonctionner l'iPad correctement avec les outils que les développeurs utilisent déjà.

## Où nous en sommes

Vysio est en bêta privée. Le retour le plus utile jusqu'ici est simple : quand le navigateur arrête de voler les raccourcis et de perdre la connexion, coder sur iPad commence à devenir normal.

Nous préparons une version publique TestFlight suivie d'une soumission sur l'App Store. Si vous souhaitez être parmi les premiers à l'essayer, rejoignez la liste d'attente sur notre page d'accueil.

L'expérience développeur sur iPad méritait mieux. C'est exactement le rôle de Vysio.
