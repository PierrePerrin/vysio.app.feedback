---
title: "Le guide complet de GitHub Codespaces sur iPad en 2026"
date: "2026-06-07"
description: "Pas à pas : configurez GitHub Codespaces, connectez-vous depuis votre iPad et contournez les limites du navigateur qui rendent le code pénible sur iPadOS."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "7 min de lecture"
---

GitHub Codespaces est l'une des meilleures façons de coder depuis un iPad, parce que l'iPad n'a pas besoin d'exécuter le projet localement. Il doit surtout afficher l'éditeur, envoyer vos frappes clavier et garder une connexion stable à la machine qui travaille.

Sur le papier, c'est simple. En pratique, le dernier mètre est le plus pénible : Safari, les raccourcis clavier, la mise en veille et les sessions GitHub. Ce guide présente une configuration réaliste pour utiliser Codespaces sur iPad, et les endroits où un client natif comme Vysio aide vraiment.

## Qu'est-ce que GitHub Codespaces ?

GitHub Codespaces est un environnement de développement cloud hébergé par GitHub. Quand vous ouvrez un Codespace, vous obtenez un conteneur tournant chez Microsoft Azure avec :

- Un éditeur VS Code complet dans le navigateur
- Un terminal Linux avec accès root
- Du stockage persistant entre les sessions
- Un environnement de développement pré-configuré basé sur le `devcontainer.json` de votre dépôt

Pour les utilisateurs iPad, l'avantage critique est que votre iPad n'a qu'à afficher l'éditeur et envoyer des frappes clavier. Toute la compilation, l'installation de paquets et l'exécution se passe dans le cloud.

Votre iPad sert surtout d'écran et de clavier. C'est le Codespace qui fait le gros du travail.

## Prérequis

- Un compte GitHub (le plan gratuit inclut 60 heures-cœur par mois)
- Un iPad sous iPadOS 17 ou ultérieur
- Un clavier externe (fortement recommandé — le clavier à l'écran vous frustrera)
- Vysio installé depuis TestFlight si vous voulez le flux iPad natif décrit plus bas

## Étape 1 : créer votre premier Codespace

Rendez-vous sur n'importe quel dépôt GitHub et cliquez sur le bouton vert **Code**. Sélectionnez l'onglet **Codespaces**, puis cliquez sur **Create codespace on main** (ou la branche sur laquelle vous souhaitez travailler).

GitHub va provisionner votre conteneur. Cela prend généralement 30 à 90 secondes au premier lancement. Les démarrages suivants sont beaucoup plus rapides car l'état du conteneur est préservé.

Une fois le provisionnement terminé, le navigateur ouvre votre Codespace dans une interface VS Code complète. Vous pouvez commencer à travailler immédiatement.

### Choisir un type de machine

Par défaut, GitHub fournit une machine 2 cœurs. Pour la plupart du développement web, c'est suffisant. Si vous travaillez avec de grandes bases de code, faites tourner plusieurs services ou faites quelque chose d'intensif en calcul, vous pouvez choisir une machine plus puissante en cliquant sur **Configure and create codespace** avant de confirmer.

Les types de machines vont de 2 à 32 cœurs. Les machines plus grandes coûtent plus d'heures-cœur, donc choisissez selon vos besoins réels.

## Étape 2 : configurer votre conteneur de développement

Un fichier `devcontainer.json` à la racine de votre dépôt dit à Codespaces quels outils installer automatiquement. Sans lui, vous obtenez un conteneur Ubuntu vide et devez tout installer manuellement à chaque fois.

Voici un exemple minimal pour un projet Node.js :

```json
{
  "name": "Node.js",
  "image": "mcr.microsoft.com/devcontainers/javascript-node:20",
  "postCreateCommand": "npm install",
  "customizations": {
    "vscode": {
      "extensions": [
        "esbenp.prettier-vscode",
        "dbaeumer.vscode-eslint"
      ]
    }
  }
}
```

Ajoutez ce fichier au dépôt, puis le prochain Codespace créé depuis ce projet pourra démarrer avec Node 20, vos dépendances npm installées et vos extensions préférées.

La [spécification Dev Container](https://containers.dev) fournit des images pré-construites pour la plupart des langages et frameworks. Vous avez rarement besoin d'écrire un Dockerfile personnalisé.

## Étape 3 : se connecter depuis l'iPad — la méthode navigateur (et ses limites)

Ouvrez Safari sur votre iPad et naviguez vers `github.com`. Connectez-vous, ouvrez votre dépôt, et lancez votre Codespace comme vous le feriez sur un Mac.

Ça fonctionne. L'interface VS Code se charge, vous pouvez parcourir les fichiers, et l'édition basique est fonctionnelle.

Voici où ça devient pénible :

**Conflits de raccourcis clavier.** Safari intercepte `Cmd + P` (imprimer), `Cmd + W` (fermer l'onglet), `Cmd + T` (nouvel onglet) et `Cmd + N` (nouvelle fenêtre) avant que VS Code puisse les recevoir. Ce ne sont pas des commandes rares. Ce sont celles qui servent à trouver des fichiers, fermer des éditeurs et ouvrir des terminaux.

**Mise en veille de l'écran.** iOS suspend agressivement les processus en arrière-plan. Si votre écran iPad s'éteint pendant une longue compilation ou exécution de tests, la connexion WebSocket à votre Codespace tombe. Quand vous rallumez l'écran, vous devez attendre la reconnexion avant de voir les résultats.

**Stockage de session.** Safari stocke votre session GitHub comme un état de navigateur. C'est normal pour naviguer sur le web, mais moins agréable quand vous essayez d'utiliser Codespaces comme un outil de travail quotidien et que vous devez vous reconnecter au mauvais moment.

Ces problèmes ne sont pas des bugs Safari. C'est le comportement normal d'un navigateur dans un usage qui attend les réflexes d'un éditeur de bureau.

## Étape 4 : se connecter avec Vysio — la méthode native

Vysio est une application iPadOS native construite pour ce cas d'usage. Elle ouvre Codespaces dans une `WKWebView` configurée et ajoute les éléments natifs que Safari ne fournit pas pour ce flux de travail.

**Installez Vysio** depuis TestFlight (lien sur la page d'accueil Vysio) et connectez-vous avec votre compte GitHub via le flux OAuth. Votre token est stocké dans le trousseau Apple, chiffré et verrouillé derrière Face ID.

**Ouvrez votre Codespace** en le sélectionnant depuis le tableau de bord natif. Vysio liste tous vos Codespaces avec leur état actuel — en cours, arrêté, ou en démarrage — et vous permet de les démarrer et arrêter sans ouvrir un navigateur.

Une fois que votre Codespace s'ouvre dans la vue éditeur de Vysio :

- `Cmd + P` ouvre le sélecteur de fichiers de VS Code
- `Cmd + W` ferme l'onglet éditeur actif
- `Cmd + T` ouvre un nouveau terminal (si configuré dans VS Code)
- `Cmd + Shift + P` ouvre la palette de commandes

Ces raccourcis passent directement à VS Code sans être interceptés par le navigateur.

L'écran reste allumé pendant qu'un espace de travail est actif. Une compilation longue peut continuer pendant que vous lisez de la documentation ou vérifiez une API, et vous retrouvez le même terminal connecté en revenant.

## Étape 5 : optimiser votre flux de travail

### Utilisez abondamment la palette de commandes VS Code

`Cmd + Shift + P` est l'un des raccourcis les plus utiles sur iPad. La plupart des actions VS Code y sont accessibles, et il fonctionne proprement dans Vysio. Apprenez à lancer des tâches, ouvrir des terminaux, changer de thème et installer des extensions depuis le clavier.

### Transfert de port pour le développement web

Quand votre serveur de développement démarre (disons sur le port 3000), Codespaces crée automatiquement un port transféré. Vous pouvez ouvrir l'URL de prévisualisation — au format `https://<nom-codespace>-3000.app.github.dev` — directement dans un onglet de navigateur ou dans une prévisualisation de port Vysio.

### Persister l'environnement entre les sessions

Codespaces sauvegarde vos fichiers ouverts et l'historique du terminal entre les sessions. Quand vous arrêtez un Codespace et le redémarrez plus tard, vous revenez approximativement là où vous étiez. C'est différent de reconstruire le conteneur — une reconstruction repart de zéro mais ré-exécute les étapes de configuration de votre `devcontainer.json`.

Arrêtez votre Codespace quand vous terminez de travailler pour éviter de consommer des heures-cœur. GitHub arrêtera aussi automatiquement les Codespaces inactifs après un délai configurable (30 minutes par défaut).

### Gérer les coûts

Le plan gratuit GitHub inclut une allocation mensuelle d'heures-cœur et de stockage. Pour un usage occasionnel, cela peut suffire ; pour un usage quotidien, vérifiez vos paramètres de facturation avant de laisser tourner une grosse machine tout l'après-midi.

Arrêtez votre Codespace quand vous avez fini, et configurez un délai d'inactivité raisonnable dans GitHub. Les machines plus puissantes sont pratiques, mais elles consomment l'allocation plus vite.

## Le résultat

Avec un Codespace configuré pour votre projet et Vysio qui gère la connexion depuis l'iPad, l'ensemble cesse de ressembler à un bricolage dans le navigateur et commence à ressembler à un vrai environnement de développement.

Votre clavier fonctionne. Votre écran reste allumé. Vos identifiants sont sécurisés. Votre code vit dans un vrai conteneur Linux avec de vrais outils.

Si vous voulez l'essayer, rejoignez la bêta TestFlight de Vysio depuis la page d'accueil.
