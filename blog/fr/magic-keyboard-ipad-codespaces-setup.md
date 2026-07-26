---
title: "Magic Keyboard + iPad + GitHub Codespaces : le guide de configuration du développeur"
date: "2026-05-31"
description: "Comment configurer un flux de développement iPad centré sur le clavier avec GitHub Codespaces, des claviers physiques et des raccourcis qui arrivent vraiment dans l'éditeur."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "6 min de lecture"
---

Si vous codez sur iPad, vous savez déjà que le clavier peut vite devenir compliqué. iPadOS gère les entrées clavier différemment de macOS, et les éditeurs cloud comme VS Code ajoutent une couche par-dessus. Le plus difficile n'est pas de taper du code. C'est de faire arriver les raccourcis que vous utilisez toute la journée dans l'éditeur, au lieu du système ou du navigateur.

Ce guide couvre les claviers qui valent le détour, les raccourcis qui comptent le plus, et l'endroit où le navigateur bloque.

## Choisir un clavier

Tous les claviers ne se comportent pas de la même façon sur iPad. Les différences comptent pour les développeurs.

### Apple Magic Keyboard pour iPad Pro

Souvent l'option la plus propre si vous possédez un iPad Pro. Il se connecte via le Smart Connector (pas de couplage Bluetooth, pas de batterie à charger), s'attache magnétiquement et inclut un trackpad qui fonctionne bien avec le pointeur d'iPadOS.

Pour le développement, l'avantage clé est qu'il dispose d'un ensemble complet de touches modificatrices — `Cmd`, `Option`, `Control`, `Shift` — et elles se comportent exactement comme vous l'attendriez d'un clavier Mac. Les touches de fonction sont disponibles via des combinaisons `Fn`.

La seule omission vraiment gênante pour les développeurs est l'absence d'une touche `Escape` dédiée. En mode Vim ou dans un terminal, `Escape` sert en permanence. Vous pouvez remapper `Caps Lock` vers `Escape` dans les Réglages iPadOS sous **Général → Clavier → Clavier physique → Touches de modification**.

### Apple Magic Keyboard (universel)

Le Magic Keyboard autonome se connecte via Bluetooth et fonctionne avec n'importe quel iPad. Il propose une disposition complète et reste familier si vous utilisez déjà un clavier Mac. Le compromis : une petite latence de connexion Bluetooth au démarrage et pas de trackpad.

Pour une configuration de bureau, il est excellent. Pour une utilisation mobile, vous perdez le support intégré des claviers folio.

### Logitech MX Keys Mini for Mac

Un clavier sans fil compact qui peut être associé à trois appareils via les boutons `Easy-Switch`. La version Mac affiche les bons libellés de touches pour iPadOS. La disposition compacte supprime le pavé numérique sans sacrifier les touches de direction, ce qui compte pour les raccourcis de navigation.

Il fonctionne sur batterie, se recharge en USB-C, propose un rétroéclairage et reste agréable pour taper longtemps. C'est un bon choix si vous passez souvent entre iPad, Mac et PC.

### Ce qu'il faut éviter

Les claviers USB Windows génériques peuvent fonctionner, mais les positions des touches modificatrices (`Ctrl`, `Alt`, `Windows`) ne correspondent pas bien aux conventions iPadOS. Vous risquez d'appuyer sur les mauvaises touches jusqu'à avoir remappé les modificateurs dans les réglages iPadOS.

Évitez les claviers Bluetooth qui nécessitent une étape de couplage par PIN — la plupart ne le font pas, mais certains modèles anciens oui, et l'iPad se recouple à chaque reconnexion, ce qui devient rapidement irritant.

## Le problème des raccourcis clavier dans les navigateurs

Voici le problème central : quand vous ouvrez VS Code dans Safari, iPadOS et Safari veulent tous deux gérer les raccourcis clavier. Ils ont la priorité. VS Code ne reçoit que ce qu'ils ne réclament pas.

Les raccourcis qu'ils réclament sont exactement ceux que vous utilisez le plus :

| Raccourci | Action iPadOS/Safari | Action souhaitée dans VS Code |
|-----------|---------------------|-------------------------------|
| `Cmd + P` | Boîte de dialogue d'impression | Ouvrir le sélecteur de fichiers |
| `Cmd + W` | Fermer l'onglet du navigateur | Fermer l'onglet de l'éditeur |
| `Cmd + T` | Nouvel onglet du navigateur | Nouveau terminal |
| `Cmd + N` | Nouvelle fenêtre du navigateur | Nouveau fichier |
| `Cmd + ,` | (variable) | Ouvrir les réglages |

Ce n'est pas un bug VS Code. Safari se comporte comme prévu. Il ne sait simplement pas que vous voulez coder.

## La solution : transfert natif des raccourcis clavier avec Vysio

Vysio résout ce problème au niveau de la couche WebKit. Au lieu d'exécuter VS Code dans Safari, Vysio l'encapsule dans un `WKWebView` personnalisé configuré pour supprimer l'interception des raccourcis au niveau système. Les événements clavier passent directement au contenu web avant qu'iPadOS puisse agir dessus.

Après avoir installé Vysio et ouvert votre Codespace via l'application, les raccourcis courants fonctionnent comme prévu :

- `Cmd + P` → sélecteur de fichiers VS Code
- `Cmd + W` → ferme l'onglet éditeur actif
- `Cmd + T` → nouveau panneau terminal
- `Cmd + N` → nouveau fichier sans titre
- `Cmd + Shift + P` → palette de commandes

Pas d'onglet Safari fermé par accident, pas de fenêtre d'impression quand vous vouliez ouvrir un fichier, et pas besoin de remapper VS Code juste pour passer une session normale.

## Les raccourcis qui comptent le plus

Une fois que le transfert des raccourcis fonctionne, concentrez-vous sur ceux-ci. Ils couvrent la plupart des gestes d'une session de code normale.

### Navigation
- `Cmd + P` — Aller à un fichier (raccourci le plus important dans VS Code)
- `Cmd + Shift + E` — Basculer l'explorateur de fichiers
- `Cmd + B` — Basculer la barre latérale
- `` Ctrl + ` `` — Basculer le terminal intégré
- `Cmd + Shift + F` — Rechercher dans tous les fichiers
- `` ` `` — Basculer entre les groupes d'éditeurs

### Édition
- `Cmd + D` — Sélectionner la prochaine occurrence du mot courant
- `Option + Clic` — Ajouter un curseur à la position cliquée
- `Cmd + Shift + K` — Supprimer la ligne
- `Option + Haut/Bas` — Déplacer la ligne vers le haut ou le bas
- `Cmd + /` — Basculer le commentaire de ligne
- `Cmd + Z` / `Cmd + Shift + Z` — Annuler / Rétablir

### Exécuter du code
- `Cmd + Shift + P` puis taper "Run Task" — déclencher n'importe quel lanceur de tâches configuré
- `` Ctrl + Shift + ` `` — Nouveau panneau terminal
- `Cmd + Shift + B` — Lancer la tâche de build

### Spécifique à VS Code
- `Cmd + K, Cmd + S` — Ouvrir l'éditeur de raccourcis clavier (utile pour les remappages)
- `Cmd + Shift + X` — Ouvrir le panneau d'extensions
- `Cmd + ,` — Ouvrir les réglages

## Gestes trackpad pour les développeurs

Si vous utilisez le Magic Keyboard avec trackpad, ces gestes accélèrent la navigation dans VS Code :

- **Défilement à deux doigts** dans l'explorateur de fichiers pour naviguer rapidement
- **Cliquer et glisser** pour sélectionner du code — plus précis que la sélection tactile
- **Clic à deux doigts (clic droit)** pour les menus contextuels dans la marge de l'éditeur
- **Balayage à trois doigts vers le haut** pour voir toutes les fenêtres ouvertes (App Exposé)

Le pointeur d'iPadOS 17+ est assez bon pour travailler au quotidien. Il ne se comporte pas exactement comme celui de macOS — les états de survol sont un peu différents, certains éléments d'interface restent pensés pour le tactile — mais ce n'est plus le point faible de la configuration.

## Disposition suggérée pour l'espace de travail

Avec un Magic Keyboard et le trackpad, vous pouvez partir sur cette disposition :

1. **Vysio en plein écran** — pas de distractions, pas de dock, pas de barre d'état visible
2. **Barre latérale de l'explorateur fermée** — utilisez `Cmd + P` pour naviguer dans les fichiers
3. **Deux colonnes d'éditeur** — fichier principal à gauche, référence ou fichier de test à droite
4. **Panneau terminal dans le tiers inférieur** — toujours visible, dimensionné pour afficher 8-10 lignes

Vous pouvez sauvegarder cette disposition en utilisant la fonctionnalité "Profils" intégrée de VS Code, pour qu'elle se restaure à chaque ouverture de Vysio.

## Écran externe

L'iPad Pro prend en charge les écrans externes via USB-C. Si vous connectez un moniteur, vous obtenez un deuxième écran dans Stage Manager. Vysio s'exécute dans sa propre fenêtre Stage Manager, donc vous pouvez garder VS Code sur l'écran externe et utiliser l'écran intégré de l'iPad pour la documentation, le terminal ou les aperçus web.

C'est là que la configuration iPad Pro cesse de ressembler à un compromis de tablette. L'écran externe peut fonctionner à sa résolution native (jusqu'à 6K sur Apple Studio Display), le trackpad contrôle les deux écrans, et Vysio maintient votre Codespace actif pendant la session.

## Une dernière chose

Rien de tout cela ne nécessite un iPad haut de gamme. Le calcul de développement se passe dans le Codespace, pas sur votre iPad. Un iPad Pro 2016 ferait tourner Vysio et afficherait VS Code tout aussi bien qu'un M4, à condition qu'il supporte iPadOS 17.

Le clavier compte plus que la puce. Choisissez-en un qui vous convient, faites fonctionner les raccourcis, puis ajustez l'espace de travail autour de ça.

Si vous voulez essayer la configuration complète, rejoignez la bêta Vysio depuis la page d'accueil.
