# Le Comptoir des Saisons - dossier de travail

## Contexte
- Restaurant traditionnel, SARL, 45 couverts, ouvert du mardi au samedi, à Dijon.
- Client du Cabinet Arcan Expertise (tenue comptable et révision).
- Depuis le 1er septembre 2026, le restaurant reçoit des factures électroniques
  via sa plateforme agréée. Les grands fournisseurs (GrossiFrais, Boissons & Co)
  envoient du Factur-X ou de l'UBL ; les petits producteurs envoient encore du PDF,
  parfois scanné.
- Toutes les données de ce dossier sont fictives.

## Organisation du dossier
- sources/ : pièces originales. NE JAMAIS LES MODIFIER, NE JAMAIS LES DÉPLACER.
  - sources/factures-structurees/ : factures Factur-X (PDF avec XML embarqué) et UBL (XML).
  - sources/factures-pdf/ : factures PDF des petits fournisseurs, y compris des scans.
  - sources/releves-bancaires/ : relevés bancaires au format CSV.
  - sources/historique-prix-aout.csv : prix d'achat du mois précédent.
- reglementaire/ : fiches de référence (TVA, mentions obligatoires). À consulter
  pour toute question de TVA ou de conformité d'une facture.
- fiches-techniques/ : composition et prix de vente des plats.
- sorties/AAAA-MM/ : tous les résultats, rangés par mois.

## Règles de travail
- Montants en euros, deux décimales, séparateur décimal virgule.
- Fichiers CSV : séparateur point-virgule, virgule décimale.
- Pour une facture Factur-X ou UBL, toujours utiliser les données XML structurées.
- Une même facture peut avoir été reçue deux fois (plateforme agréée et courriel) :
  toujours rechercher les doublons par fournisseur, numéro et montant.
- Une anomalie se signale, elle ne se corrige jamais dans les sources.
- Si une information est illisible ou incertaine, le dire explicitement et
  proposer une hypothèse vérifiable, sans la présenter comme un fait.
- Les résultats sont rédigés en Markdown.

## Procédures disponibles (skills)
- controle-facture : vérification des factures fournisseurs.
- cout-matiere : suivi des prix d'achat et coût matière des plats.
- traitement-mensuel : traitement complet d'un mois (contrôle, rapprochement,
  analyse, livrables).

## Spécialistes disponibles (sous-agents)
- controleur-tva : toute vérification de taux de TVA sur des factures d'achat.
- analyste-achats : analyse des variations de prix et du coût matière.

## Destinataires des résultats
- La gérante : tableau de bord clair, sans jargon comptable, avec des actions concrètes.
- Le cabinet : note de révision technique, anomalies classées par gravité,
  impacts chiffrés.
