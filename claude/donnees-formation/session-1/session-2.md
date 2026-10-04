# Session 2 : Déléguer un travail à Claude

## Objectifs de la session

À la fin de cette session, vous saurez :

- rédiger une procédure en Markdown, compréhensible par un agent ;
- la faire exécuter par Claude sur un ensemble de documents ;
- corriger la procédure à partir des erreurs constatées ;
- transformer une procédure validée en *skill* réutilisable ;
- appliquer cette méthode à un besoin réel.

## Rappel : où en sommes-nous ?

Lors de la session 1, nous avons vu qu'un agent se programme avec trois briques : `CLAUDE.md`, les skills et les sous-agents. Aujourd'hui, nous construisons les **skills**. Dans la structure du dossier final, nous remplissons cette partie :

```text
Comptoir-des-Saisons/
`-- .claude/
    `-- skills/
        |-- controle-facture/    fil rouge Cabinet
        `-- cout-matiere/        fil rouge Restaurant
```

## 1. Les données de la session

Le dossier `session-2/` contient les achats de septembre 2026 du Comptoir des Saisons :

| Fournisseur | Activité | Format reçu | Nombre de factures |
|---|---|---|---|
| GrossiFrais | Grossiste alimentaire (grande entreprise) | Factur-X | 4 |
| Boissons & Co | Distributeur de boissons (ETI) | UBL (XML) | 2 |
| Ferme des Trois Chênes | Producteur (micro-entreprise) | PDF | 2 |
| Le Potager de Léon | Maraîcher | PDF scanné | 2 |
| Fromagerie du Vallon | Artisan fromager | PDF | 1 |
| Clim'Hotte Services | Maintenance de la hotte | PDF | 1 |

S'y ajoutent :

- `historique-prix-aout.csv` : les prix d'achat du mois précédent ;
- `fiches-techniques/` : la composition de cinq plats de la carte ;
- `reglementaire/tva-restauration.md` : une fiche de référence sur les taux de TVA.

> Ces documents contiennent volontairement quelques anomalies. À vous, et à Claude, de les trouver.

### Un mot sur les factures électroniques

Une facture **Factur-X** ressemble à un PDF ordinaire, mais elle contient en plus un fichier XML qui reprend toutes les données de la facture sous une forme structurée. Une facture **UBL** est directement un fichier XML. Pour un agent, ces formats sont une excellente nouvelle : les montants, taux et références sont lus sans erreur de lecture, contrairement à un PDF scanné.

## 2. Rédiger une procédure

### La méthode

Une bonne procédure pour un agent contient cinq parties :

1. **L'objectif** : à quoi sert le travail, pour qui ;
2. **Les sources** : quels documents utiliser ;
3. **Les étapes** : numérotées, dans l'ordre ;
4. **Les règles** : ce qu'il faut toujours faire, ce qu'il ne faut jamais faire ;
5. **Le résultat attendu** : le format précis de la sortie.

### Fil rouge Cabinet : le contrôle des factures

Voici un point de départ. Nous allons le compléter ensemble.

```markdown
# Contrôle des factures fournisseurs

## Objectif
Vérifier les factures fournisseurs du mois pour préparer la révision
du dossier du Comptoir des Saisons.

## Sources
- Les factures du dossier session-2 (formats structurés et PDF).
- La fiche reglementaire/tva-restauration.md.

## Étapes
1. Lister toutes les factures avec fournisseur, numéro, date et format.
2. Pour chaque facture, recalculer les lignes et les totaux.
3. Vérifier le taux de TVA de chaque ligne avec la fiche de référence.
4. Vérifier les mentions obligatoires.
5. Repérer les doublons éventuels.

## Règles
- Ne jamais modifier une facture.
- Pour une facture structurée, utiliser les données XML.
- En cas de doute, signaler plutôt que conclure.

## Résultat attendu
1. Un tableau récapitulatif des factures (HT, TVA par taux, TTC).
2. Un tableau des anomalies : facture, nature, gravité, action proposée.
```

### Fil rouge Restaurant : le suivi des prix et le coût matière

```markdown
# Suivi des prix d'achat et coût matière

## Objectif
Aider la gérante à suivre l'évolution de ses prix d'achat et
le coût matière de ses plats.

## Sources
- Les factures du dossier session-2.
- Le fichier historique-prix-aout.csv.
- Les fiches techniques des plats.

## Étapes
1. Extraire de chaque facture les produits, quantités et prix unitaires HT.
2. Comparer chaque prix avec le prix d'août.
3. Calculer le coût matière de chaque plat avec les prix de septembre.
4. Comparer le coût matière au prix de vente HT du plat.

## Règles
- Ramener tous les prix à la même unité (kg, litre, pièce).
- Signaler toute hausse supérieure à 10 %.

## Résultat attendu
1. Un tableau des variations de prix, trié de la plus forte hausse
   à la plus forte baisse.
2. Un tableau du coût matière par plat, avec le ratio
   coût matière / prix de vente HT.
3. Trois recommandations courtes pour la gérante.
```

## 3. Exécuter, observer, corriger

### L'exercice

1. Connectez le dossier `session-2/` dans Claude.
2. Enregistrez la procédure du fil rouge Cabinet dans un fichier `procedure-controle.md`.
3. Demandez à Claude : *« Applique la procédure procedure-controle.md aux factures de septembre. »*
4. Vérifiez le résultat : a-t-il trouvé toutes les anomalies ? S'est-il trompé quelque part ?
5. **Corrigez la procédure, pas le résultat.** Si Claude a mal appliqué un taux, c'est souvent que la règle n'était pas assez explicite.
6. Relancez et comparez.

Recommencez avec la procédure du fil rouge Restaurant.

### Le réflexe essentiel

Quand l'agent se trompe, la tentation est de corriger le tableau à la main. C'est une erreur : la même erreur reviendra le mois prochain. **Corrigez la consigne**, c'est elle qui constitue votre programme.

| Erreur constatée | Correction à apporter à la procédure |
|---|---|
| Un taux de TVA mal vérifié | Préciser la règle dans la fiche de référence ou dans les règles |
| Une unité mal convertie | Ajouter une règle de conversion explicite |
| Une anomalie non détectée | Ajouter une étape de contrôle dédiée |
| Un résultat mal présenté | Décrire plus précisément le format attendu |

### Les modes de validation

Pendant la formation, laissez Claude en **validation manuelle** : il vous demande votre accord avant chaque action. Vous voyez ainsi ce qu'il s'apprête à faire, ce qui est très instructif. Les modes plus autonomes sont à réserver aux tâches maîtrisées, sur des données sans risque.

## 4. Transformer une procédure en skill

### Pourquoi une skill ?

Une procédure dans un fichier, il faut penser à la donner à Claude. Une **skill**, Claude la connaît : il sait qu'elle existe et l'applique dès qu'une demande correspond à sa description. Elle devient une compétence permanente de votre agent.

### La structure d'une skill

Une skill est un dossier qui porte son nom et qui contient au minimum un fichier `SKILL.md` :

```text
controle-facture/
|-- SKILL.md                 la procédure
`-- modele-rapport.md        un modèle de rapport (facultatif)
```

Le fichier `SKILL.md` commence par un en-tête entre deux lignes de tirets :

```markdown
---
name: controle-facture
description: Contrôle des factures fournisseurs (calculs, TVA,
  mentions obligatoires, doublons). À utiliser dès qu'il faut
  vérifier ou réviser des factures d'achat.
---

# Contrôle des factures fournisseurs

(la procédure validée)
```

**La description est décisive** : c'est elle que Claude lit pour décider d'utiliser la skill. Elle doit dire **ce que fait** la skill et **quand** l'utiliser.

### L'exercice

1. Demandez à Claude de transformer votre procédure validée en skill : *« Transforme procedure-controle.md en skill nommée controle-facture. »*
2. Relisez le fichier `SKILL.md` obtenu, en particulier la description.
3. Ajoutez la skill à Claude, dans la rubrique des paramètres consacrée aux skills (le libellé exact peut varier selon votre version).
4. Testez-la dans une nouvelle conversation, sans mentionner la procédure : *« Vérifie les factures de septembre du Comptoir des Saisons. »*

Faites de même pour la skill `cout-matiere`.

## 5. Atelier : votre propre besoin

Reprenez la tâche que vous avez notée à la fin de la session 1 et appliquez la méthode :

1. Rédigez la procédure en cinq parties ;
2. Testez-la sur des données fictives ;
3. Corrigez-la au moins une fois.

Si vous n'avez pas de données fictives adaptées, demandez à Claude d'en générer : c'est une utilisation très efficace, et sans risque.

## Récapitulatif de la session

- Une procédure efficace contient : objectif, sources, étapes, règles, résultat attendu.
- Quand l'agent se trompe, on **corrige la consigne**, pas le résultat.
- Une **skill** est une procédure validée, rangée dans un dossier, avec une description qui indique quand l'utiliser.
- Les skills que vous avez créées aujourd'hui seront réutilisées telles quelles dans Claude Code.

## Pour la prochaine session

Conservez précieusement les dossiers de vos deux skills (`controle-facture` et `cout-matiere`) : ils seront au cœur de la session 3.
