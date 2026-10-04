# Contrôle des factures fournisseurs

> Version complétée de la procédure du fil rouge Cabinet, telle qu'elle peut
> ressortir de la rédaction collective de la session 2.

## Objectif
Vérifier les factures fournisseurs du mois pour préparer la révision du dossier
du Comptoir des Saisons.

## Sources
- Les factures du dossier factures/ (formats structurés et PDF).
- La fiche reglementaire/tva-restauration.md.
- La fiche reglementaire/mentions-obligatoires.md.

## Étapes
1. Lister toutes les factures avec fournisseur, numéro, date, échéance et format.
2. Pour chaque facture, recalculer les lignes (quantité × prix unitaire) et les totaux.
3. Vérifier le taux de TVA de chaque ligne avec la fiche de référence.
4. Vérifier les mentions obligatoires, en particulier les pénalités de retard
   et l'indemnité forfaitaire de 40 €.
5. Repérer les doublons éventuels (même fournisseur, même numéro, même montant).

## Règles
- Ne jamais modifier une facture.
- Pour une facture structurée (Factur-X, UBL), utiliser les données XML.
- Pour un scan, signaler toute zone illisible au lieu de deviner.
- En cas de doute, signaler plutôt que conclure.

## Résultat attendu
1. Un tableau récapitulatif des factures (HT, TVA par taux, TTC).
2. Un tableau des anomalies : facture, nature, impact en euros, gravité,
   action proposée.
