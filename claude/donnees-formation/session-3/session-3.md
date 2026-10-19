# Support d'exercices


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

**L'exercice.** 

1. Demandez à cClaude uin premier bourillon en rédigeant un CLAUDE.md à partir de la structure du dossier
2. Rédigez votre `CLAUDE.md` à partir de ce modèle, puis ouvrez une nouvelle session et demandez simplement : *« Que sais-tu de ce dossier ? »* La réponse montre ce que l'agent a retenu.

## 4. Créer des sous-agents

**Le format d'un sous-agent**

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

**L'exercice.** 

1. Créez le sous-agent `controleur-tva`
2. puis, sur le même principe, le sous-agent `analyste-achats` (spécialiste des variations de prix et du coût matière). Vous pouvez demander à Claude de rédiger le second en s'inspirant du premier.

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

