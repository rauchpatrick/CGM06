---
name: controle-facture
description: Contrôle des factures fournisseurs du Comptoir des Saisons (recalcul
  des lignes et des totaux, taux de TVA, mentions obligatoires, doublons). À utiliser
  dès qu'il faut vérifier, contrôler ou réviser des factures d'achat.
---

# Contrôle des factures fournisseurs

## Objectif
Vérifier les factures fournisseurs d'une période pour préparer la révision du
dossier par le cabinet, et repérer ce qui doit être réclamé aux fournisseurs.

## Sources
- Les factures de sources/factures-structurees/ et sources/factures-pdf/.
- reglementaire/tva-restauration.md et reglementaire/mentions-obligatoires.md.

## Étapes
1. Inventorier toutes les factures : fournisseur, numéro, date, échéance, format
   (Factur-X, UBL, PDF, PDF scanné), canal présumé (plateforme ou courriel).
2. Pour une facture Factur-X ou UBL, lire les données XML. Pour un PDF, lire le
   document ; pour un scan, signaler toute zone illisible.
3. Recalculer chaque ligne : quantité × prix unitaire HT = montant HT.
4. Recalculer la base et la TVA par taux, puis les totaux HT, TVA et TTC.
5. Vérifier le taux de TVA de chaque ligne avec la fiche de référence
   (déléguer au sous-agent controleur-tva s'il est disponible).
6. Vérifier les mentions obligatoires avec la fiche de référence. Ne pas signaler
   l'absence des nouvelles mentions de la facturation électronique sur les
   factures PDF des petits fournisseurs.
7. Rechercher les doublons : même fournisseur, même numéro ou même montant.

## Règles
- Ne jamais modifier une facture.
- Une anomalie se signale avec son impact chiffré, même faible.
- En cas de doute, signaler plutôt que conclure.

## Résultat attendu
Utiliser le modèle modele-rapport.md, placé dans le dossier de cette skill.
