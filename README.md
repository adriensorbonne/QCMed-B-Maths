# QCM B · Maths

Site de révision des **mathématiques du QCM** de l'épreuve écrite d'admissibilité n° 2 du **concours externe de Contrôleur des Finances Publiques**.

Le site propose des cours courts appuyés sur des exemples concrets, des exercices corrigés, une calculatrice scientifique et des PDF de cours à télécharger. Il s'adresse aux candidats qui préparent le concours, en particulier à ceux que les maths découragent : l'objectif est de comprendre la méthode plutôt que de la réciter.

> Le programme du concours comporte quatre blocs : connaissances générales, français, **mathématiques** et raisonnement logique. Ce site ne couvre que le bloc mathématiques (manipulation des nombres et algèbre).

## Ce que contient le site

Le site tient dans un seul fichier, `index.html`. Il comporte cinq onglets.

### Cours

- 28 chapitres courts, à lire dans l'ordre ou en sautant d'un chapitre à l'autre.
- Une machine interactive en page d'accueil illustre la notion de fonction (f(x) = 2x).
- Les chapitres couvrent :
  - **Nombres :** ensembles de nombres, multiples et diviseurs, critères de divisibilité, nombres premiers, nombres premiers entre eux, division euclidienne, valeur décimale et approchée, puissances et notation scientifique.
  - **Proportionnalité et pourcentages :** produit en croix, TVA.
  - **Algèbre :** développement et factorisation, identités remarquables, équations et inéquations du 1er degré, systèmes de deux équations (substitution et combinaison).
  - **Analyse :** fonctions, dérivée, primitives et intégrales. Cette partie relève du programme du QRC, la seconde partie de l'épreuve.

### Exercices

Deux sous-onglets :

- **Exos QCM :** 92 questions à choix multiples, avec correction immédiate et méthode. Un filtre par cours et un score permettent de s'entraîner par thème.
- **Exos Usuels :** 39 exercices rédigés, issus de fiches de travail, regroupés par thème (factorisation, problèmes du 1er degré, PGCD et divisibilité, division euclidienne, systèmes, second degré, etc.). L'énoncé s'affiche d'abord, la correction détaillée s'ouvre à la demande.

### Calculatrice

Une calculatrice scientifique intégrée : priorités opératoires, puissances, racines, fonctions trigonométriques, logarithmes, factorielle, pourcentages, notation scientifique, résultat précédent (Rép) et historique. Elle sert pendant un exercice sans quitter le site : les réponses et la place dans les exercices sont conservées quand on change d'onglet.

### PDFs

Un PDF par chapitre de cours, généré à la demande et téléchargeable, pour réviser hors connexion ou imprimer.

### Programme

Rappel de la structure de l'épreuve et détail du programme de mathématiques, avec un repère « cours disponible » sur chaque point déjà couvert. Les cours sont ajoutés au fur et à mesure.

## Sections liées

L'onglet Cours propose deux liens vers des sections séparées, chacune dans son propre fichier : **Réviser la spé maths du B** (`SpeMathsB.html`) et **Réviser la spé maths du A** (`SpeMathsA.html`). Elles reprennent les mêmes onglets (Cours, Exercices, Calculatrice, Programme, PDFs). Chacune propose un lien « Retour au site QCM B ». Les trois fichiers doivent se trouver dans le même dossier.

## Confort d'utilisation

- Mode clair et mode sombre (le choix est mémorisé).
- Interface adaptée au mobile : barre d'onglets fixée en bas de l'écran, liste des chapitres repliable, zones tactiles agrandies.
- Navigation au clavier et attributs d'accessibilité de base (focus visible, rôles ARIA).
- Pas de compte à créer côté serveur : tout fonctionne dans le navigateur.

## Accès

Une page de connexion demande un identifiant (le prénom) et un mot de passe commun. La session est conservée tant que l'onglet reste ouvert.

**Cette protection est légère, pas sécurisée.** La vérification se fait dans le navigateur (empreinte SHA-256 du mot de passe, présente dans le code). Elle sert à limiter l'accès à un groupe de candidats, pas à protéger des données sensibles : le contenu des cours reste lisible dans le code source de la page. Une liste d'identifiants autorisés est prévue dans le code (`ALLOWED`), mais elle est vide : seul le mot de passe est contrôlé.

## Technique

| Point | Détail |
|---|---|
| Format | Un seul fichier HTML avec CSS et JavaScript intégrés, sans framework ni serveur |
| Données | Les cours, exercices et corrections sont des tableaux JavaScript dans le fichier |
| Stockage | `localStorage` pour le thème, `sessionStorage` pour la session |
| PDF | Génération côté navigateur avec `html2canvas` et `jsPDF`, chargés à la demande depuis cdnjs |
| Hors connexion | Fonctionne sans réseau, sauf la génération des PDF (bibliothèques chargées à la volée) |

Les PDF sont des images de pages : le texte n'y est pas sélectionnable. Ce choix garantit l'affichage correct des symboles mathématiques (ℕ, ², √, ⊂, φ, ∫).

## Utiliser ou héberger le site

- **En local :** ouvrir le fichier HTML dans un navigateur récent.
- **En ligne :** déposer le fichier sur n'importe quel hébergement de pages statiques. La page ne dépend d'aucun serveur applicatif.

## Ajouter du contenu

Tout se trouve dans la balise `<script>` du fichier.

**Un cours** : ajouter un objet dans le tableau `COURSES`.

```js
{t:"Titre du cours", s:"Sous-titre (thème)", h:
"<h2>Titre</h2>"+
"<p>Texte…</p>"+
"<div class=\"formula\">Formule à retenir</div>"},
```

Le cours apparaît automatiquement dans la liste des chapitres et dans l'onglet PDFs.

**Un exercice QCM** : ajouter un objet dans le tableau `EXOS` (`c` = catégorie du filtre, `o` = les choix, `a` = indice de la bonne réponse, `e` = explication).

```js
{c:"Proportionnalité", q:"Question ?", o:["A","B","C","D"], a:1, e:"Explication."},
```

**Un exercice usuel** : ajouter un objet `{t, q, a}` (titre, énoncé, correction) dans le groupe voulu du tableau `USU`.

**Le programme** : mettre à jour l'onglet Programme à la main (repère « cours disponible ») et la liste `UPCOMING` des cours à venir.

## Limites connues

- Le contrôle d'accès n'est pas sécurisé (voir plus haut).
- Les PDF générés ne contiennent pas de texte sélectionnable.
- Le site couvre les mathématiques du QCM uniquement : pas de culture générale, de français ni de raisonnement logique.
- Certains points du programme n'ont pas encore de cours : PGCD et PPCM détaillés, monômes et polynômes, intérêts simples, prix d'achat, de vente et de revient, masses et densité.
- Des énoncés issus de fiches peuvent contenir des coquilles : en cas de doute sur une correction, se reporter à l'énoncé d'origine.
