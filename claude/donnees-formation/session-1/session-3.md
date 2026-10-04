# Session 3 : Structurer et automatiser avec Claude Code

## Objectifs de la session

À la fin de cette session, vous saurez :

- organiser un dossier de travail pour un agent ;
- rédiger un fichier `CLAUDE.md` complet ;
- installer vos skills dans Claude Code ;
- créer un sous-agent spécialisé ;
- lancer un traitement complet par une seule demande.

## Rappel : où en sommes-nous ?

| Brique | Session | Statut |
|---|---|---|
| Skills `controle-facture` et `cout-matiere` | 2 | Rédigées et testées dans Claude |
| Structure du dossier | 3 | Aujourd'hui |
| `CLAUDE.md`, le chef d'orchestre | 3 | Aujourd'hui |
| Sous-agents | 3 | Aujourd'hui |

## 1. Démarrer avec Claude Code

Nous utilisons l'onglet **Code** de l'application Claude Desktop. Il offre les mêmes fonctions que Claude Code en terminal, avec une interface graphique.

1. Ouvrez l'application Claude Desktop et choisissez l'onglet **Code**.
2. Sélectionnez le dossier `Comptoir-des-Saisons/` fourni par le formateur. Il contient déjà les sources, mais ni `CLAUDE.md`, ni skills, ni sous-agents.
3. Au premier lancement, Claude vous demande de confirmer que vous faites confiance à ce dossier : acceptez, puisqu'il s'agit de votre dossier d'exercices.

> Comme en session 2, gardez la **validation manuelle** des actions : Claude vous demande l'autorisation avant de créer ou modifier un fichier.

## 2. Construire la structure du dossier

Voici la structure cible, présentée en session 1 :

```text
Comptoir-des-Saisons/
|-- CLAUDE.md
|-- sources/
|   |-- factures-structurees/
|   |-- factures-pdf/
|   `-- releves-bancaires/
|-- reglementaire/
|-- fiches-techniques/
|-- sorties/
`-- .claude/
    |-- skills/
    |   |-- controle-facture/
    |   |-- cout-matiere/
    |   `-- traitement-mensuel/
    `-- agents/
        |-- controleur-tva.md
        `-- analyste-achats.md
```

Chaque dossier a un rôle précis :

| Dossier | Rôle | Règle |
|---|---|---|
| `sources/` | Les pièces originales | L'agent les lit, ne les modifie jamais |
| `reglementaire/` | Les références (TVA, mentions obligatoires) | Mises à jour par vous seulement |
| `fiches-techniques/` | Les recettes et grammages | Données de gestion du restaurant |
| `sorties/` | Tout ce que produit l'agent | Un sous-dossier par mois |
| `.claude/skills/` | Les procédures | Une skill par dossier |
| `.claude/agents/` | Les sous-agents | Un fichier par spécialiste |

**L'exercice.** Demandez à Claude de compléter la structure : *« Crée les dossiers manquants de cette arborescence, sans déplacer les fichiers existants. »* Puis copiez vos deux skills de la session 2 dans `.claude/skills/`.

> Le dossier `.claude` commence par un point : il est donc masqué par défaut sous Windows et macOS. Pensez à afficher les fichiers cachés dans votre explorateur.

## 3. Rédiger le fichier `CLAUDE.md`

### Le rôle du chef d'orchestre

`CLAUDE.md` est lu automatiquement à chaque session. C'est lui qui transforme un dossier rangé en un **agent qui sait travailler** : il donne le contexte, fixe les règles, décrit l'organisation et indique quelles skills et quels sous-agents mobiliser.

Une astuce : Claude Code peut proposer un premier brouillon de `CLAUDE.md` en analysant votre dossier. Vous le relisez et le complétez ensuite. Dans tous les cas, **c'est vous qui en êtes l'auteur** : ce fichier traduit vos règles de travail.

### Un modèle complet

```markdown
# Le Comptoir des Saisons - dossier de travail

## Contexte
- Restaurant traditionnel, SARL, 45 couverts, ouvert du mardi au samedi.
- Client du Cabinet Arcan Expertise (tenue et révision).
- Depuis le 1er septembre 2026, le restaurant reçoit des factures
  électroniques via sa plateforme agréée. Les grands fournisseurs
  envoient du Factur-X ou de l'UBL, les petits producteurs du PDF.

## Organisation du dossier
- sources/ : pièces originales. NE JAMAIS LES MODIFIER.
- reglementaire/ : fiches de référence, à consulter pour toute
  question de TVA ou de mentions obligatoires.
- fiches-techniques/ : composition des plats.
- sorties/AAAA-MM/ : tous les résultats, rangés par mois.

## Règles de travail
- Montants en euros, deux décimales, séparateur décimal virgule.
- Pour une facture structurée, toujours utiliser les données XML.
- Une anomalie se signale, elle ne se corrige pas.
- En cas de doute, poser la question plutôt que supposer.
- Les résultats sont rédigés en Markdown.

## Procédures disponibles
- controle-facture : vérification des factures fournisseurs.
- cout-matiere : suivi des prix d'achat et coût matière des plats.
- traitement-mensuel : traitement complet d'un mois.

## Spécialistes disponibles
- controleur-tva : toute vérification de taux de TVA.
- analyste-achats : analyse des prix et du coût matière.

## Destinataires des résultats
- La gérante : tableau de bord clair, sans jargon comptable.
- Le cabinet : note de révision technique, anomalies classées par gravité.
```

**L'exercice.** Rédigez votre `CLAUDE.md` à partir de ce modèle, puis ouvrez une nouvelle session et demandez simplement : *« Que sais-tu de ce dossier ? »* La réponse montre ce que l'agent a retenu.

## 4. Créer des sous-agents

### Pourquoi déléguer ?

Un sous-agent travaille dans son propre espace, avec ses propres instructions. Cela présente deux avantages :

- **la spécialisation** : le sous-agent a des consignes précises, limitées à son domaine ;
- **la clarté** : l'agent principal reçoit un résultat synthétique, sans être encombré par tous les détails intermédiaires.

### Le format d'un sous-agent

Un sous-agent est un simple fichier Markdown rangé dans `.claude/agents/`. Comme une skill, il commence par un en-tête qui indique son nom et quand l'utiliser.

```markdown
---
name: controleur-tva
description: Spécialiste de la TVA en restauration. À utiliser pour
  vérifier les taux de TVA appliqués sur des factures d'achat.
---

Tu es un collaborateur spécialisé en TVA dans un cabinet
d'expertise comptable.

## Ta mission
Vérifier, ligne par ligne, le taux de TVA appliqué sur chaque facture
d'achat qui t'est confiée.

## Ta méthode
1. Identifier la nature de chaque produit ou service.
2. Déterminer le taux applicable à l'aide de reglementaire/.
3. Comparer avec le taux facturé.
4. Calculer l'impact financier de chaque écart.

## Ce que tu rends
Un tableau : facture, ligne, produit, taux facturé, taux attendu,
écart en euros, commentaire.
Tu ne conclus jamais sans avoir consulté la fiche de référence.
```

**L'exercice.** Créez le sous-agent `controleur-tva`, puis, sur le même principe, le sous-agent `analyste-achats` (spécialiste des variations de prix et du coût matière). Vous pouvez demander à Claude de rédiger le second en s'inspirant du premier.

## 5. Le traitement complet en une demande

### La skill d'orchestration

Il reste à créer une dernière skill, qui enchaîne tout le travail du mois. C'est elle qui fait du dossier un véritable traitement automatisé.

```markdown
---
name: traitement-mensuel
description: Traitement complet des achats d'un mois pour le
  Comptoir des Saisons. À utiliser quand on demande de traiter
  les factures ou les achats d'un mois donné.
---

# Traitement mensuel des achats

1. Inventorier les factures du mois dans sources/.
2. Appliquer la skill controle-facture à l'ensemble des factures.
3. Confier la vérification des taux au sous-agent controleur-tva.
4. Rapprocher les factures du relevé bancaire du mois.
5. Confier l'analyse des prix et du coût matière au sous-agent
   analyste-achats.
6. Produire dans sorties/AAAA-MM/ :
   - tableau-de-bord.md, destiné à la gérante ;
   - note-revision.md, destinée au cabinet.
7. Terminer par un résumé de cinq lignes maximum.
```

### Le lancement

Dans une nouvelle session, tapez simplement :

> Traite les achats de septembre 2026.

Observez Claude : il lit `CLAUDE.md`, reconnaît la skill `traitement-mensuel`, enchaîne les étapes, délègue aux sous-agents et range les résultats. Vous pouvez aussi appeler la skill directement en tapant `/traitement-mensuel`.

### La vérification

L'automatisation ne dispense pas du contrôle. Relisez les deux documents produits :

- le **tableau de bord** est-il compréhensible par la gérante ?
- la **note de révision** relève-t-elle toutes les anomalies placées dans les données ?

Si ce n'est pas le cas, vous savez désormais où agir : dans `CLAUDE.md` pour une règle générale, dans une skill pour une procédure, dans un sous-agent pour une spécialité.

## 6. Atelier : vos cas personnels

Reprenez le besoin travaillé en fin de session 2 et posez-vous trois questions :

1. Quelle **structure de dossier** lui conviendrait ?
2. Quelles **règles permanentes** iraient dans `CLAUDE.md` ?
3. Une partie du travail mériterait-elle un **sous-agent** spécialisé ?

## 7. Aller plus loin

- **Les tâches planifiées** : Claude peut exécuter des tâches récurrentes à intervalle régulier. À réserver à des tâches simples, sur des données sans risque, avec une relecture systématique des résultats.
- **Le partage en équipe** : skills et sous-agents peuvent être regroupés en *plugins* et partagés dans une organisation, ce qui permet de diffuser une méthode commune.
- **Le passage en production** : abonnement professionnel, validation par le DPO, inscription au registre des traitements, information des équipes. Relisez la partie RGPD de la session 1.

## Récapitulatif de la formation

| Ce que vous avez appris | Où cela se trouve dans le dossier |
|---|---|
| Écrire une procédure claire | Les skills, dans `.claude/skills/` |
| Fixer le contexte et les règles | `CLAUDE.md` |
| Déléguer à un spécialiste | Les sous-agents, dans `.claude/agents/` |
| Organiser les sources et les résultats | `sources/`, `reglementaire/`, `sorties/` |

Le message essentiel : **programmer un agent, c'est rédiger et organiser**. Vous savez déjà écrire des procédures, des programmes de travail et des fiches de contrôle. Avec ces outils, ces documents deviennent directement exécutables.
