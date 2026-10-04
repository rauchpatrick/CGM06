---
name: cout-matiere
description: Suivi des prix d'achat et calcul du coût matière des plats du Comptoir
  des Saisons. À utiliser pour toute question sur l'évolution des prix fournisseurs,
  les hausses de prix, le coût d'un plat ou la rentabilité de la carte.
---

# Suivi des prix d'achat et coût matière

## Objectif
Aider la gérante à suivre l'évolution de ses prix d'achat et le coût matière de
ses plats, pour ajuster ses achats ou ses prix de vente.

## Sources
- Les factures du mois dans sources/.
- sources/historique-prix-aout.csv : prix du mois précédent.
- fiches-techniques/ : composition et prix de vente des plats.

## Étapes
1. Extraire de chaque facture les produits, quantités et prix unitaires HT.
2. Ramener chaque prix à l'unité de référence de l'historique (kg, L, pièce...).
3. Retenir, pour chaque produit, le dernier prix connu du mois.
4. Comparer avec le prix d'août et calculer la variation en pourcentage.
5. Pour chaque fiche technique, convertir les quantités (g, cl, fraction de pièce)
   dans l'unité d'achat et calculer le coût matière d'une portion.
6. Calculer le ratio coût matière / prix de vente HT.

## Règles
- Conversions : 1 kg = 1 000 g ; 1 L = 100 cl ; bidon de crème = 5 L ;
  bouteille de vin = 75 cl ; plateau d'œufs = 30 œufs.
- Une variation n'est significative que si les deux prix sont exprimés dans la
  même unité : vérifier les conditionnements avant de conclure.
- Signaler toute hausse supérieure à 10 %.
- Les prix sont toujours hors taxes.

## Résultat attendu
1. Un tableau des variations de prix, trié de la plus forte hausse à la plus
   forte baisse, avec les alertes au-dessus de 10 %.
2. Un tableau du coût matière par plat : coût d'une portion, prix de vente HT,
   ratio en pourcentage.
3. Trois recommandations courtes et concrètes pour la gérante.
