# Session 1 : Comprendre l'IA agentique et démarrer

## Objectifs de la session

À la fin de cette session, vous saurez :

- expliquer la différence entre une conversation avec une IA, un Projet ou un GPT, et un agent ;
- décrire les trois briques qui permettent de « programmer » un agent : le fichier `CLAUDE.md`, les *skills* et les sous-agents ;
- lire et écrire un document simple en Markdown ;
- distinguer Claude (ex-Cowork) et Claude Code ;
- savoir où partent vos données et quelles règles respecter ;
- lancer une première tâche dans Claude.

## 1. Qu'est-ce que l'IA agentique ?

### Trois façons de travailler avec une IA

**La conversation.** Vous posez une question, l'IA répond. Vous copiez la réponse, vous la collez ailleurs, vous reposez une question. C'est vous qui faites tout le travail d'organisation : l'IA ne voit que ce que vous lui donnez, et elle ne fait rien d'autre que répondre.

**Le Projet (ou le GPT personnalisé).** Vous donnez à l'IA des instructions permanentes et quelques documents de référence. Elle répond mieux, car elle connaît votre contexte. Mais elle reste dans la conversation : elle ne va pas chercher un fichier, ne crée pas un tableau Excel dans votre dossier et ne vérifie pas son propre travail.

**L'agent.** Vous confiez une **mission**, pas une question. L'agent dispose d'outils : il peut lire les fichiers d'un dossier, en créer de nouveaux, exécuter des calculs, consulter le web. Il découpe la mission en étapes, les exécute, contrôle le résultat et corrige si nécessaire, jusqu'à ce que la mission soit terminée.

| | Conversation | Projet / GPT | Agent |
|---|---|---|---|
| Ce que vous donnez | Une question | Une question + un contexte permanent | Une mission |
| Ce que l'IA produit | Une réponse | Une réponse mieux adaptée | Un travail terminé (fichiers, tableaux, notes) |
| Accès à vos fichiers | Ceux que vous collez | Quelques documents de référence | Un dossier entier |
| Qui organise le travail | Vous | Vous | L'agent |
| Vérification | Par vous | Par vous | Par l'agent, puis par vous |

**==> Démonstration**

### La boucle de l'agent

Un agent fonctionne selon une boucle simple, qui ressemble beaucoup à la façon dont travaille un collaborateur :


```
+----------------------+       +-------------------+
| 1.Mission & contexte |------>| 2. Plannification |
+----------------------+       +-------------------+
            ^                           |
            |                           |
            |                           v
+----------------------+       +------------------+
|    4. Vérification   |<------|    3. Action     |
+----------------------+       +------------------+
```



1. **Comprendre** la mission et le contexte ;
2. **Planifier** les étapes ;
3. **Agir** : lire un fichier, faire un calcul, écrire un document ;
4. **Vérifier** le résultat ;
5. **Recommencer** l'étape suivante, ou corriger si quelque chose ne va pas.

Une comparaison utile : un Projet, c'est un expert à qui vous posez des questions. Un agent, c'est un collaborateur à qui vous confiez un dossier.

### Programmer un agent : trois briques essentielles

Un agent bien « programmé » ne repose pas sur une consigne géniale tapée au clavier. Il repose sur des **fichiers écrits en français**, rangés dans un dossier. Trois briques sont essentielles.

#### Le fichier `CLAUDE.md` : le "chef d'orchestre"

`CLAUDE.md` est un fichier texte placé à la racine de votre dossier de travail. Claude le lit **automatiquement au début de chaque session**. Il contient tout ce que l'agent doit savoir en permanence :

- le contexte (qui est le client, quelle est son activité) ;
- les règles à respecter (taux de TVA, conventions de nommage, format des sorties) ;
- l'organisation du dossier (où trouver les sources, où ranger les résultats) ;
- les procédures disponibles et quand les utiliser.

C'est la **partition du chef d'orchestre** : l'agent principal la lit, puis il sait quelles procédures appliquer et à quels spécialistes confier chaque partie du travail. Sans `CLAUDE.md`, il faut tout réexpliquer à chaque fois. Avec lui, une simple demande comme « traite les factures de septembre » suffit.

Voici à quoi ressemble un `CLAUDE.md` très simplifié :

```markdown
# Le Comptoir des Saisons - dossier de travail

## Contexte
Restaurant traditionnel (SARL), 45 couverts, client du Cabinet Arcan Expertise.

## Règles
- Les montants sont toujours exprimés en euros, avec deux décimales.
- Ne jamais modifier les fichiers du dossier sources/.
- Toujours signaler une anomalie plutôt que la corriger soi-même.

## Organisation
- Les factures sont dans sources/.
- Les résultats sont enregistrés dans sorties/.
```

#### La *skill* : une procédure réutilisable

Une *skill* (compétence) est une **procédure écrite**, rangée dans son propre dossier, que l'agent sait appliquer quand la situation s'y prête. Elle contient un fichier principal `SKILL.md` et, si besoin, des modèles ou des exemples.

Chaque skill commence par une courte description. C'est grâce à elle que Claude sait **quand** utiliser la skill : si vous lui demandez de contrôler une facture et qu'une skill décrit justement le contrôle des factures, il l'applique automatiquement. Vous pouvez aussi l'appeler directement par son nom.

Une skill, c'est l'équivalent d'une **fiche de procédure du cabinet** : on l'écrit une fois, on l'améliore au fil du temps, et tout le monde l'applique de la même façon.

```markdown
---
name: controle-facture
description: Contrôle une facture fournisseur (mentions obligatoires,
  calculs, taux de TVA). À utiliser pour toute vérification de facture.
---

# Contrôle d'une facture fournisseur

1. Vérifier la présence des mentions obligatoires.
2. Recalculer chaque ligne : quantité × prix unitaire.
3. Vérifier le taux de TVA appliqué à chaque produit.
4. Recalculer les totaux HT, TVA et TTC.
5. Lister les anomalies dans un tableau.
```

#### Le sous-agent : un spécialiste à qui déléguer

Un sous-agent est un **assistant spécialisé** que l'agent principal peut appeler pour une partie précise du travail. Il a son propre rôle, ses propres instructions et travaille dans son propre espace : il revient avec un résultat, sans encombrer la mémoire de l'agent principal.

Dans un cabinet, c'est l'équivalent de l'organisation d'une mission : le chef de mission répartit le travail, un collaborateur s'occupe de la TVA, un autre du rapprochement bancaire, puis le chef de mission fait la synthèse.

| Brique      | Rôle                                                       | Comparaison avec un cabinet                       |
| ----------- | ---------------------------------------------------------- | ------------------------------------------------- |
| `CLAUDE.md` | Contexte et règles permanentes, organisation du travail    | La lettre de mission et les règles internes       |
| Skill       | Une procédure précise, réutilisable                        | Une fiche de procédure ou un programme de travail |
| Sous-agent  | Un spécialiste à qui l'on délègue une partie de la mission | Un collaborateur spécialisé de l'équipe           |

### Où allons-nous ? La structure du dossier final

À la fin de la session 3, nous aurons construit ensemble le dossier suivant. Ne cherchez pas à tout comprendre aujourd'hui : gardez simplement cette carte en tête, nous la remplirons étape par étape.

```text
Comptoir-des-Saisons/
|-- CLAUDE.md                   le chef d'orchestre
|-- sources/                    les pièces, jamais modifiées
|   |-- factures-structurees/   factures électroniques (Factur-X, UBL)
|   |-- factures-pdf/           factures des petits fournisseurs
|   `-- releves-bancaires/
|-- reglementaire/              fiches de référence (TVA, mentions obligatoires)
|-- fiches-techniques/          recettes et grammages des plats
|-- sorties/                    ce que produit l'agent
`-- .claude/
    |-- skills/                 les procédures réutilisables
    |   |-- controle-facture/
    |   `-- cout-matiere/
    `-- agents/                 les sous-agents spécialisés
        |-- controleur-tva.md
        `-- analyste-achats.md
```

Ce dossier **est** le programme. Il ne contient aucune ligne de code : uniquement des documents rédigés en français, bien rangés. C'est ce qu'on appelle programmer un agent en langage naturel.

---
## Comprendre le token

C'est le facteur qui peut limiter l'usage :
* Minimiser les échanges pour éviter les hallucinations ou des traitements trop "libres"
* Trop de tokens tuent l'ia

Texte en français :

>## Qu'est-ce que le Lorem Ipsum?
>Le **Lorem Ipsum** est simplement du faux texte employé dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l'imprimerie depuis les années 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour réaliser un livre spécimen de polices de texte. Il n'a pas fait que survivre cinq siècles, mais s'est aussi adapté à la bureautique informatique, sans que son contenu n'en soit modifié. Il a été popularisé dans les années 1960 grâce à la vente de feuilles Letraset contenant des passages du Lorem Ipsum, et, plus récemment, par son inclusion dans des applications de mise en page de texte, comme Aldus PageMaker.

**Découpage en tokens par l'IA**

<img src="./ressources/capture-20260924-101507.png">

**Transformation en vecteur**

<img src="./ressources/capture-20260924-101539.png">

**La vallée des probabilités!**

<img src="./ressources/visuel_puits_statistiques.jpeg">

```
		  CARTE DU SENS : chaque mot est un point

  ┌─ Travail du bois ──────┐        ┌─ Boulangerie ──────────┐
  │        • ébéniste      │        │    • boulanger         │
  │       /                │        │          • pâtissier   │
  │  (•) MENUISIER         │        │                        │
  │   |     \              │        │   • croissant          │
  │ • charpentier • parquet│        │            • farine    │
  └────────────────────────┘        └────────────────────────┘

  ┌─ Plomberie ────────────┐        ┌─ Coiffure ─────────────┐
  │   • plombier           │        │  • coiffeur            │
  │          • chauffe-eau │        │            • brushing  │
  │                        │        │                        │
  │ • fuite    • robinet   │        │ • frange   • shampoing │
  └────────────────────────┘        └────────────────────────┘

  Vecteur de « menuisier » (simplifié à 8 nombres) :
  [ 0.99, -0.10, 0.41, -0.48, 0.03, 0.54, -0.65, -0.04, … ]

   0.99  ████████████
  -0.10  ▒
   0.41  █████
  -0.48  ▒▒▒▒▒▒
   0.03  ▏
   0.54  ███████
  -0.65  ▒▒▒▒▒▒▒▒
  -0.04  ▏

  Plus proches voisins : ébéniste, charpentier, parquet
  (un vrai modèle utilise de 768 à plus de 3 000 nombres)
```

<!--
Pour vos artisans, trois idées suffisent à comprendre.

**Le vecteur est une adresse de sens.** « Menuisier » et « ébéniste » ont des listes de nombres très semblables, donc ils sont voisins sur la carte. « Menuisier » et « shampoing » sont très éloignés. L'IA ne compare pas les lettres des mots, elle compare leurs positions. C'est pourquoi elle comprend qu'une « fuite sous l'évier » concerne un plombier, même si le mot « plombier » n'apparaît pas.

**Une base de données vectorielle est un entrepôt de ces adresses.** On y range chaque document de l'entreprise (fiches techniques, devis types, FAQ clients) découpé en morceaux, chacun avec son vecteur. Quand on pose une question, elle est elle-même transformée en vecteur, et la base renvoie les morceaux les plus proches sur la carte. C'est une recherche par le sens, et non par mots-clés.

**Une analogie qui parle aux artisans : l'atelier bien rangé.** Dans une base classique, les outils sont classés par ordre alphabétique : le rabot est loin de la varlope. Dans une base vectorielle, ils sont rangés par usage : tout ce qui sert à dégauchir est sur la même étagère. On y trouve donc ce qu'on cherche même si on ne connaît pas le nom exact de l'outil.

C'est exactement ce qui se passe quand un stagiaire donne un long document à ChatGPT ou Claude, ou utilise un espace projet : l'outil va chercher les passages proches de la question avant de répondre. Cela se nomme le RAG (génération augmentée par récupération).
-->


---


## 2. Un outil indispensable : le format Markdown

### Pourquoi le Markdown ?

Le Markdown est une façon d'écrire du texte avec quelques symboles simples pour indiquer la mise en forme : titres, listes, gras, tableaux. Il est indispensable pour trois raisons :

- **c'est la langue naturelle des agents** : Claude lit et écrit le Markdown parfaitement, et tous les fichiers de configuration (`CLAUDE.md`, skills, sous-agents) sont en Markdown ;
- **la structure est visible** : les titres et les listes aident l'agent à comprendre l'organisation d'une procédure, comme ils aident un lecteur humain ;
- **c'est un format ouvert et durable** : un simple fichier texte, lisible avec n'importe quel logiciel, convertible en Word, PDF ou page web.

### L'essentiel de la syntaxe

| Vous écrivez | Vous obtenez |
|---|---|
| `# Titre` | Un titre de niveau 1 |
| `## Sous-titre` | Un titre de niveau 2 |
| `**important**` | Du texte en **gras** |
| `*nuance*` | Du texte en *italique* |
| `- élément` | Une liste à puces |
| `1. étape` | Une liste numérotée |
| `> remarque` | Une citation ou un encadré |
| `` `sorties/` `` | Un nom de fichier ou de dossier |

Un tableau s'écrit ainsi :

```markdown
| Fournisseur | Format | Montant TTC |
|---|---|---|
| GrossiFrais | Factur-X | 1 248,60 |
| Ferme des Trois Chênes | PDF | 312,00 |
```

### La bonne pratique : écrire comme pour un nouveau collaborateur

Une consigne efficace pour un agent ressemble à une bonne fiche de procédure : un objectif clair, des étapes numérotées, des règles explicites et le résultat attendu. Si un stagiaire pouvait suivre votre procédure sans vous poser de question, un agent le pourra aussi.

**==> Exercice pratique**

## 3. Claude (ex-Cowork) et Claude Code

Les deux outils reposent sur le même moteur agentique. Ce qui change, c'est l'environnement de travail et la façon de réutiliser les consignes.

### Claude (anciennement Claude Cowork)

Claude Cowork est désormais simplement appelé **Claude** : vous formulez votre demande, et Claude décide s'il s'agit d'une réponse rapide ou d'une tâche à mener. Ce changement est déployé progressivement selon les abonnements, l'interface peut donc encore varier d'un participant à l'autre.

Concrètement :

- vous travaillez dans l'application Claude Desktop, avec une interface graphique ;
- vous connectez un ou plusieurs dossiers de votre ordinateur ;
- Claude lit vos fichiers, produit des documents (Excel, Word, PowerPoint, Markdown) et peut utiliser vos applications ;
- vous réutilisez vos procédures sous forme de skills.

C'est l'outil de la **délégation assistée** : vous confiez la tâche et vous la supervisez.

### Claude Code

Claude Code travaille directement dans un dossier de votre ordinateur. Nous l'utiliserons via l'onglet **Code** de l'application Claude Desktop, sans passer par un terminal. Il donne accès à toute la puissance de l'organisation en dossiers : `CLAUDE.md`, skills, sous-agents.

C'est l'outil de l'**automatisation** : une fois le dossier construit, une seule demande déclenche un traitement complet.

### En résumé

| | Claude (ex-Cowork) | Claude Code |
|---|---|---|
| Interface | Application de bureau, conversationnelle | Onglet Code de l'application (ou terminal) |
| Public | Tous les utilisateurs | Utilisateurs prêts à structurer un dossier |
| Où s'exécute le travail | Dans le cloud d'Anthropic, avec accès à vos dossiers connectés | Sur votre ordinateur |
| Réutilisation | Skills | `CLAUDE.md`, skills, sous-agents |
| Logique | Déléguer et superviser | Structurer et automatiser |

Les skills sont communes aux deux outils : une procédure rédigée en session 2 pour Claude sera réutilisée telle quelle en session 3 dans Claude Code.

## 4. RGPD et traitement des données

> Les informations ci-dessous sont à jour en octobre 2026. Les conditions des éditeurs évoluent vite : vérifiez-les avant tout déploiement, avec le DPO de votre structure.

### Le critère décisif : le type d'abonnement

**Abonnements grand public (Free, Pro, Max).** Ils relèvent des conditions d'utilisation grand public et ne comportent **pas d'accord de sous-traitance (DPA)**. Les échanges peuvent servir à l'entraînement des modèles si l'option correspondante est activée, avec une conservation des données pouvant aller jusqu'à cinq ans. Ces abonnements ne conviennent pas au traitement de données personnelles pour le compte d'une entreprise.

**Abonnements professionnels (Team, Enterprise, API).** Un DPA est automatiquement inclus dans les conditions commerciales. Anthropic agit comme **sous-traitant**, votre structure reste **responsable de traitement**, et les données ne servent pas à l'entraînement.

> Pour un usage réel en cabinet ou en entreprise : **jamais de compte personnel** pour des données professionnelles.

### Le transfert hors de l'Union européenne

Les traitements d'Anthropic ont lieu sur une infrastructure située aux États-Unis. Le transfert est encadré par les clauses contractuelles types et le Data Privacy Framework. Un traitement dans l'Union européenne reste possible pour Claude Code, en le configurant pour utiliser Claude via un fournisseur cloud dans une région européenne (Amazon Bedrock, par exemple).

### Où sont traitées les données dans chaque outil ?

**Dans Claude (ex-Cowork)**, les sessions s'exécutent dans un environnement isolé, sur les serveurs d'Anthropic. Les fichiers locaux que Claude ouvre via l'application sont donc traités sur ces serveurs, et ne restent pas uniquement sur votre ordinateur.

**Dans Claude Code**, les commandes s'exécutent sur votre ordinateur, mais tout ce que Claude lit (contenu des fichiers, résultats de calculs) est envoyé au modèle pour être analysé.

Dans les deux cas, **tout fichier que l'agent lit quitte votre poste**. C'est la règle à retenir.

### La traçabilité

Les abonnements professionnels offrent des outils de suivi (journaux d'audit, API de conformité, télémétrie). Leur couverture de Claude (ex-Cowork) et de Claude Code s'est beaucoup étendue en 2026, mais elle dépend de l'abonnement et de la configuration. C'est un point à vérifier avec votre service informatique avant un usage réel.

### Les points propres à vos métiers

- **Secret professionnel** : experts-comptables et commissaires aux comptes y sont tenus. Toute utilisation sur des données clients doit s'inscrire dans un cadre contractuel adapté (abonnement professionnel, DPA) et dans la politique de votre structure.
- **Données des salariés** : plannings, bulletins, arrêts maladie relèvent du RGPD, et certaines sont des données sensibles. Une analyse d'impact (AIPD) peut être nécessaire.
- **Registre des traitements** : l'outil doit y être inscrit.
- **Instances représentatives** : l'introduction d'une nouvelle technologie peut nécessiter l'information ou la consultation du CSE.
- **Durées de conservation** : un document transmis à un outil d'IA ne doit pas être conservé au-delà de ce que prévoit votre politique.

### Facture électronique et plateforme agréée

La plateforme agréée reste **le canal officiel** de réception des factures électroniques. L'agent n'intervient pas dans ce circuit : il travaille sur des **exports ou des copies**. L'original électronique, avec sa valeur probante, reste dans la plateforme.

### Les règles de cette formation

1. Données exclusivement fictives.
2. Un dossier de travail dédié, sans accès à vos dossiers professionnels.
3. Validation manuelle des actions de Claude (mode par défaut).

## 5. Première prise en main

### L'exercice

Dans le dossier d'exercices, ouvrez le sous-dossier `session-1/`. Il contient trois factures fictives du Comptoir des Saisons :

- une facture électronique structurée d'un grossiste alimentaire ;
- une facture PDF d'un producteur local ;
- une facture PDF d'un prestataire de maintenance.

**Étape 1.** Dans l'application Claude, connectez le dossier `session-1/` et tapez simplement :

> Analyse ces factures.

Observez le résultat. Qu'a fait Claude ? Qu'a-t-il choisi de regarder ?

**Étape 2.** Recommencez dans une nouvelle conversation avec une consigne structurée :

```markdown
# Mission
Tu es collaborateur dans un cabinet d'expertise comptable.
Analyse les trois factures du dossier session-1.

# Pour chaque facture
1. Identifie le fournisseur, la date et le format (structuré ou PDF).
2. Relève les montants HT, TVA et TTC.
3. Vérifie que les calculs sont justes.
4. Indique le ou les taux de TVA appliqués.

# Résultat attendu
Un tableau récapitulatif, puis la liste des anomalies éventuelles.
```

**Étape 3.** Comparez les deux résultats.

### À retenir

La différence entre les deux résultats ne vient pas de l'outil, mais de la consigne. Une consigne structurée en Markdown produit un travail plus complet, plus fiable et plus facile à vérifier. Lors de la session 2, nous transformerons ce type de consigne en procédure réutilisable.

## Récapitulatif de la session

- Un agent reçoit une **mission**, pas une question, et organise lui-même son travail.
- On programme un agent avec trois briques écrites en français : **`CLAUDE.md`** (le chef d'orchestre), les **skills** (les procédures) et les **sous-agents** (les spécialistes).
- Le **Markdown** est la langue commune entre vous et l'agent.
- **Claude (ex-Cowork)** permet de déléguer et superviser, **Claude Code** permet de structurer et d'automatiser.
- Pour le RGPD, tout se joue sur **l'abonnement** et sur **ce que vous donnez à lire** à l'agent.

## Pour la prochaine session

Repérez dans votre travail une tâche répétitive, liée à des documents, que vous aimeriez confier à un agent. Notez-la en quelques lignes : nous nous en servirons en fin de session 2.
