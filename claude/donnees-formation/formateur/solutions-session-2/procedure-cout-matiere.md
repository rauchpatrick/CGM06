# Suivi des prix d'achat et coût matière

> Version complétée de la procédure du fil rouge Restaurant, telle qu'elle peut
> ressortir de la rédaction collective de la session 2.

## Objectif
Aider la gérante à suivre l'évolution de ses prix d'achat et le coût matière de
ses plats.

## Sources
- Les factures du dossier factures/.
- Le fichier historique-prix-aout.csv.
- Les fiches techniques des plats.

## Étapes
1. Extraire de chaque facture les produits, quantités et prix unitaires HT.
2. Ramener chaque prix à l'unité de l'historique (kg, L, pièce).
3. Comparer chaque prix avec le prix d'août.
4. Calculer le coût matière de chaque plat avec les prix de septembre.
5. Comparer le coût matière au prix de vente HT du plat.

## Règles
- Ramener tous les prix à la même unité : 1 kg = 1 000 g, 1 L = 100 cl,
  bidon de crème = 5 L, bouteille de vin = 75 cl, plateau d'œufs = 30 œufs.
- Retenir le dernier prix connu du mois.
- Signaler toute hausse supérieure à 10 %.

## Résultat attendu
1. Un tableau des variations de prix, trié de la plus forte hausse
   à la plus forte baisse.
2. Un tableau du coût matière par plat, avec le ratio
   coût matière / prix de vente HT.
3. Trois recommandations courtes pour la gérante.
