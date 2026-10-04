# Corrigé du jeu de données - Le Comptoir des Saisons, septembre 2026

> Document réservé au formateur. Ne pas diffuser aux participants, ne pas placer dans un dossier ouvert avec Claude pendant les exercices.

## 1. Inventaire des factures

| Fournisseur | N° | Date | Échéance | Format | HT | TVA | TTC | Sessions |
|---|---|---|---|---|---|---|---|---|
| Boissons & Co SA | BC-2026-004521 | 03/09/2026 | 18/09/2026 | UBL (XML) | 550,06 | 92,60 | 642,66 | 2, 3 |
| GrossiFrais SAS | FA2026-18734 | 04/09/2026 | 14/09/2026 | Factur-X | 341,70 | 28,64 | 370,34 | 1, 2, 3 |
| EARL Ferme des Trois Chênes | FTC-2026-031 | 05/09/2026 | 05/09/2026 | PDF | 138,40 | 7,61 | 146,01 | 2, 3 |
| Le Potager de Léon | 2026-118 | 06/09/2026 | 13/09/2026 | PDF scanné | 179,50 | 9,87 | 189,37 | 2, 3 |
| GrossiFrais SAS | FA2026-19102 | 11/09/2026 | 21/09/2026 | Factur-X | 238,74 | 13,13 | 251,87 | 2, 3 |
| GrossiFrais SAS | FA2026-19102 (copie courriel) | 11/09/2026 | 21/09/2026 | PDF simple | 238,74 | 13,13 | 251,87 | 2, 3 |
| Fromagerie du Vallon | FV-2026-0912 | 12/09/2026 | 20/09/2026 | PDF | 222,70 | 44,54 | 267,24 | 2, 3 |
| Clim'Hotte Services | CHS-2026-0457 | 16/09/2026 | 16/09/2026 | PDF | 380,00 | 76,00 | 456,00 | 1, 2, 3 |
| Boissons & Co SA | BC-2026-004987 | 17/09/2026 | 02/10/2026 | UBL (XML) | 359,36 | 65,85 | 425,21 | 2, 3 |
| GrossiFrais SAS | FA2026-19488 | 18/09/2026 | 28/09/2026 | Factur-X | 288,00 | 15,84 | 303,84 | 2, 3 |
| EARL Ferme des Trois Chênes | FTC-2026-034 | 19/09/2026 | 19/09/2026 | PDF | 117,60 | 6,47 | 124,07 | 1, 2, 3 |
| Le Potager de Léon | 2026-127 | 20/09/2026 | 27/09/2026 | PDF scanné | 166,30 | 9,15 | 175,45 | 2, 3 |
| GrossiFrais SAS | FA2026-19861 | 25/09/2026 | 05/10/2026 | Factur-X | 240,69 | 16,67 | 257,36 | 2, 3 |

Total des 12 factures distinctes : **3 223,05 € HT**, 386,37 € de TVA, **3 609,42 € TTC** (hors doublon).

Les trois factures de la session 1 sont la Factur-X GrossiFrais FA2026-18734, la facture PDF FTC-2026-034 de la Ferme des Trois Chênes (sans anomalie) et la facture Clim'Hotte CHS-2026-0457 (mentions manquantes).

## 2. Les anomalies placées

| N° | Facture | Anomalie | Impact chiffré | Gravité | Action attendue |
|---|---|---|---|---|---|
| 1 | Fromagerie du Vallon FV-2026-0912 | Fromages facturés à 20 % au lieu de 5,5 % | TVA facturée 44,54 € au lieu de 12,25 € : **32,29 €** de TVA non déductible ; TTC payé 267,24 € au lieu de 234,95 € | Haute | Demander une facture rectificative et le remboursement du trop-payé |
| 2 | Boissons & Co BC-2026-004987 | Eau minérale plate (48 × 0,48 = 23,04 € HT) facturée à 20 % au lieu de 5,5 % | TVA 4,61 € au lieu de 1,27 € : **3,34 €** | Haute | Facture rectificative avant le prélèvement du 02/10 ; comparer avec BC-2026-004521 où l'eau est correctement à 5,5 % |
| 3 | GrossiFrais FA2026-19102 | Même facture reçue via la plateforme (Factur-X) **et** par courriel (PDF avec tampon « COPIE ») | Risque de double comptabilisation : 251,87 € TTC | Moyenne | Ne retenir que la Factur-X ; vérifier dans le relevé que le prélèvement n'a eu lieu qu'une fois (c'est le cas, le 21/09) |
| 4 | Ferme des Trois Chênes FTC-2026-031 | Ligne œufs : 6 × 7,50 = 45,00 €, facturée 48,00 € | HT 138,40 € au lieu de 135,40 € ; TTC 146,01 € au lieu de 142,85 € : **3,16 €** trop payés | Moyenne | Demander un avoir ; la facture a été réglée le 08/09 pour le montant erroné |
| 5 | Clim'Hotte Services CHS-2026-0457 | Absence du taux des pénalités de retard et de l'indemnité forfaitaire de 40 € | Pas d'impact financier ; amende possible pour le fournisseur | Faible | Signaler au fournisseur ; pas de remise en cause de la déduction de TVA |
| 6 | Le Potager de Léon 2026-127 (scan) | Montant de la ligne champignons masqué par une tache | Recalcul possible : 12 × 4,90 = 58,80 €, cohérent avec le total HT lisible de 166,30 € | Faible | Signaler comme illisible, proposer l'hypothèse recalculée en la présentant comme telle |
| 7 | GrossiFrais (toutes factures) | Beurre doux : 11,56 €/kg contre 9,80 €/kg en août | **+18,0 %** | Alerte gestion | Alerter la gérante, envisager un autre fournisseur ou un ajustement des recettes |
| 8 | GrossiFrais FA2026-18734 et FA2026-19488 | Huile d'olive : 9,97 €/L contre 8,90 €/L en août | **+12,0 %** | Alerte gestion | Alerter la gérante |
| 9 | GrossiFrais (crème) | Crème achetée en bidon de 5 L à 21,75 € en septembre, en brique de 1 L à 4,20 € en août | Variation réelle : 4,35 €/L, soit **+3,6 %** et non +418 % | Piège | Vérifier que l'agent convertit l'unité avant de conclure |

Pièges secondaires sans anomalie, utiles pour le débriefing :

- les pommes Reine des Reinettes passent de 2,40 à 2,60 €/kg (+8,3 %) : hausse réelle mais **sous le seuil** de 10 % ;
- la facture BC-2026-004521 contient à la fois des boissons à 20 % et à 5,5 %, toutes correctement taxées ;
- les factures GrossiFrais mêlent denrées à 5,5 % et produits d'entretien à 20 %, tous correctement taxés ;
- les factures PDF des petits fournisseurs ne portent pas le SIREN du client ni la catégorie de l'opération : ce n'est **pas** une anomalie à ce stade (voir la fiche mentions-obligatoires.md).

## 3. Variations de prix attendues (septembre / août)

| Produit | Fournisseur | Unité | Août | Septembre | Variation | Alerte |
|---|---|---|---|---|---|---|
| Beurre doux 82 % MG - plaque 1 kg | GrossiFrais SAS | kg | 9,80 | 11,56 | 18,0 % | **oui** |
| Huile d'olive vierge extra | GrossiFrais SAS | L | 8,90 | 9,97 | 12,0 % | **oui** |
| Pommes Reine des Reinettes | Le Potager de Léon | kg | 2,40 | 2,60 | 8,3 % |  |
| Pommes de terre Agata | Le Potager de Léon | kg | 1,05 | 1,10 | 4,8 % |  |
| Champignons de Paris | Le Potager de Léon | kg | 4,70 | 4,90 | 4,3 % |  |
| Crème liquide 35 % MG | GrossiFrais SAS | L | 4,20 | 4,35 | 3,6 % |  |
| Eau minérale gazeuse 1 L | Boissons & Co SA | bouteille | 0,60 | 0,62 | 3,3 % |  |
| Mâcon-Villages blanc AOC 75 cl | Boissons & Co SA | bouteille | 6,95 | 7,10 | 2,2 % |  |
| Bière blonde pression - fût 30 L | Boissons & Co SA | fût | 96,00 | 98,00 | 2,1 % |  |
| Poulet fermier Label Rouge | EARL Ferme des Trois Chênes | kg | 9,60 | 9,80 | 2,1 % |  |
| Comté AOP 18 mois | Fromagerie du Vallon | kg | 24,00 | 24,50 | 2,1 % |  |
| Épaule de veau désossée | GrossiFrais SAS | kg | 16,50 | 16,80 | 1,8 % |  |
| Parmigiano Reggiano AOP 24 mois | GrossiFrais SAS | kg | 22,00 | 22,40 | 1,8 % |  |
| Roquefort AOP | Fromagerie du Vallon | kg | 26,50 | 26,90 | 1,5 % |  |
| Pâte feuilletée pur beurre | GrossiFrais SAS | kg | 6,70 | 6,80 | 1,5 % |  |
| Riz arborio | GrossiFrais SAS | kg | 3,40 | 3,45 | 1,5 % |  |
| Farine de blé T55 | GrossiFrais SAS | kg | 0,92 | 0,92 | 0,0 % |  |
| Riz long grain | GrossiFrais SAS | kg | 1,85 | 1,85 | 0,0 % |  |
| Sucre semoule | GrossiFrais SAS | kg | 1,10 | 1,10 | 0,0 % |  |
| Fond blanc de volaille déshydraté | GrossiFrais SAS | kg | 14,20 | 14,20 | 0,0 % |  |
| Liquide vaisselle professionnel 5 L | GrossiFrais SAS | unité | 12,50 | 12,50 | 0,0 % |  |
| Dégraissant four et hotte 5 L | GrossiFrais SAS | unité | 18,90 | 18,90 | 0,0 % |  |
| Sacs poubelle 110 L (carton de 200) | GrossiFrais SAS | carton | 24,00 | 24,00 | 0,0 % |  |
| Gants nitrile (boîte de 100) | GrossiFrais SAS | boîte | 7,90 | 7,90 | 0,0 % |  |
| Côtes-du-Rhône rouge AOC 75 cl | Boissons & Co SA | bouteille | 6,20 | 6,20 | 0,0 % |  |
| Eau minérale plate 1 L | Boissons & Co SA | bouteille | 0,48 | 0,48 | 0,0 % |  |
| Jus de pomme artisanal 1 L | Boissons & Co SA | bouteille | 2,10 | 2,10 | 0,0 % |  |
| Café en grains pur arabica 1 kg | Boissons & Co SA | kg | 16,50 | 16,50 | 0,0 % |  |
| Sirop de grenadine 1 L | Boissons & Co SA | bouteille | 4,80 | 4,80 | 0,0 % |  |
| Œufs plein air - plateau de 30 | EARL Ferme des Trois Chênes | plateau | 7,50 | 7,50 | 0,0 % |  |
| Lait entier cru | EARL Ferme des Trois Chênes | L | 1,20 | 1,20 | 0,0 % |  |
| Fromage blanc fermier | EARL Ferme des Trois Chênes | kg | 4,60 | 4,60 | 0,0 % |  |
| Carottes | Le Potager de Léon | kg | 1,40 | 1,40 | 0,0 % |  |
| Oignons jaunes | Le Potager de Léon | kg | 1,30 | 1,30 | 0,0 % |  |
| Salade batavia | Le Potager de Léon | pièce | 1,10 | 1,10 | 0,0 % |  |
| Herbes fraîches (botte) | Le Potager de Léon | botte | 0,90 | 0,90 | 0,0 % |  |
| Brie de Meaux AOP | Fromagerie du Vallon | kg | 15,80 | 15,80 | 0,0 % |  |
| Bûche de chèvre affinée | Fromagerie du Vallon | kg | 19,20 | 19,20 | 0,0 % |  |

## 4. Coût matière attendu par plat (prix de septembre)

| Plat | Coût matière d'une portion | Prix de vente HT | Ratio |
|---|---|---|---|
| Blanquette de veau à l'ancienne | 4,23 € | 21,82 € | 19,4 % |
| Risotto crémeux aux champignons | 2,16 € | 17,73 € | 12,2 % |
| Tarte fine aux pommes | 1,07 € | 8,18 € | 13,0 % |
| Assiette de fromages affinés | 2,60 € | 10,91 € | 23,8 % |
| Omelette fermière, pommes sautées | 1,42 € | 13,18 € | 10,8 % |

Détail des calculs :

- **Blanquette de veau à l'ancienne** : Épaule de veau 3,360 € ; Carottes 0,070 € ; Champignons de Paris 0,196 € ; Oignons jaunes 0,039 € ; Crème liquide 35 % 0,174 € ; Beurre doux 0,116 € ; Farine T55 0,009 € ; Fond blanc de volaille 0,114 € ; Riz long grain (garniture) 0,148 €.
- **Risotto crémeux aux champignons** : Riz arborio 0,310 € ; Champignons de Paris 0,588 € ; Parmigiano Reggiano 0,560 € ; Beurre doux 0,173 € ; Oignons jaunes 0,026 € ; Vin blanc (Mâcon-Villages) 0,284 € ; Fond blanc de volaille 0,114 € ; Huile d'olive 0,100 €.
- **Tarte fine aux pommes** : Pâte feuilletée pur beurre 0,544 € ; Pommes Reine des Reinettes 0,390 € ; Beurre doux 0,116 € ; Sucre semoule 0,016 €.
- **Assiette de fromages affinés** : Comté AOP 18 mois 0,735 € ; Brie de Meaux AOP 0,474 € ; Bûche de chèvre 0,576 € ; Roquefort AOP 0,538 € ; Salade batavia 0,275 €.
- **Omelette fermière, pommes sautées** : Œufs plein air 0,750 € ; Lait entier 0,024 € ; Pommes de terre Agata 0,165 € ; Beurre doux 0,116 € ; Herbes fraîches 0,090 € ; Salade batavia 0,275 €.

Les ratios sont volontairement bas (fiches simplifiées, sans pain, assaisonnements ni pertes). Point pédagogique utile : la hausse de 18 % du beurre touche quatre plats sur cinq, mais ne représente que 2 à 3 centimes par portion (10 à 15 g de beurre). Une forte hausse sur un produit ne signifie pas une forte hausse du coût d'un plat : c'est exactement ce que la gérante doit savoir lire.

## 5. Rapprochement bancaire attendu (relevé au 30/09/2026)

| Facture | TTC | Date de paiement | Mode | Statut |
|---|---|---|---|---|
| Boissons & Co SA BC-2026-004521 | 642,66 | 18/09 | Prélèvement | Payée |
| GrossiFrais SAS FA2026-18734 | 370,34 | 14/09 | Prélèvement | Payée |
| EARL Ferme des Trois Chênes FTC-2026-031 | 146,01 | 08/09 | Virement | Payée (montant erroné de la facture, voir anomalie 4) |
| Le Potager de Léon 2026-118 | 189,37 | 10/09 | Virement | **Écart de 15,00 €** : payé 174,37 € pour 189,37 € facturés |
| GrossiFrais SAS FA2026-19102 | 251,87 | 21/09 | Prélèvement | Payée **une seule fois** malgré le doublon |
| Fromagerie du Vallon FV-2026-0912 | 267,24 | 18/09 | Virement | Payée (TVA erronée incluse, voir anomalie 1) |
| Clim'Hotte Services CHS-2026-0457 | 456,00 | 22/09 | Virement | Payée |
| Boissons & Co SA BC-2026-004987 | 425,21 | - | - | Non payée, **non échue** (prélèvement prévu le 02/10) - à corriger avant (anomalie 2) |
| GrossiFrais SAS FA2026-19488 | 303,84 | 28/09 | Prélèvement | Payée |
| EARL Ferme des Trois Chênes FTC-2026-034 | 124,07 | - | - | **Non payée, échue depuis le 19/09** : à relancer ou à régler |
| Le Potager de Léon 2026-127 | 175,45 | 25/09 | Chèque n° 0004718 | Payée - rapprochement **présumé** par le montant, le chèque ne porte pas de nom |
| GrossiFrais SAS FA2026-19861 | 257,36 | - | - | Non payée, **non échue** (prélèvement prévu le 05/10) |

Solde du compte au 30/09/2026 : 45 304,32 €. Les autres opérations du relevé (loyer, URSSAF, énergie, salaires, remises CB, espèces) n'ont pas de facture dans le dossier : l'agent doit les identifier comme hors périmètre, sans les signaler comme anomalies.

## 6. Ce qu'on attend des livrables de la session 3

- **tableau-de-bord.md** (gérante) : total des achats du mois, alertes beurre et huile d'olive, coût matière des cinq plats, actions concrètes (réclamer à la Fromagerie du Vallon et à la Ferme des Trois Chênes, régler la facture FTC-2026-034, vérifier le virement au Potager de Léon, contacter Boissons & Co avant le 02/10).
- **note-revision.md** (cabinet) : récapitulatif des 12 factures, neutralisation du doublon, anomalies 1 à 6 classées par gravité avec leur impact, rapprochement bancaire complet, point sur la TVA déductible à retenir.

Si l'agent signale la crème comme une hausse de plus de 400 %, oublie le doublon, ou présente le montant taché comme certain, c'est l'occasion de montrer où corriger : règle de conversion dans la skill cout-matiere, règle des doublons dans CLAUDE.md, règle d'incertitude dans CLAUDE.md.
