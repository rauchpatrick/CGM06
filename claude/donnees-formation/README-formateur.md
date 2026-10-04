# Jeu de données de la formation - Le Comptoir des Saisons

Toutes les données sont **fictives** : entreprises, numéros SIREN, SIRET et TVA, adresses, IBAN et montants ont été inventés pour la formation. Les numéros respectent les règles de format (clé de contrôle) pour ne pas créer de fausses anomalies, mais ne correspondent à aucune entreprise connue.

## Ce qu'il faut envoyer, et à quel moment

| Dossier | Destinataires | Quand l'envoyer |
|---|---|---|
| `session-1/` | Participants | Avant la session 1 (créneau technique) |
| `session-2/` | Participants | Après la session 1, une fois le fil rouge Restaurant adapté si besoin |
| `session-3/Comptoir-des-Saisons/` | Participants | Après la session 2 |
| `formateur/` | **Vous seul** | Ne jamais diffuser |

## Contenu par session

### Session 1 : première prise en main

Trois factures, à connecter dans Claude pour l'exercice « consigne brute / consigne structurée » :

- `GrossiFrais_FA2026-18734.pdf` : facture électronique **Factur-X** (PDF avec le fichier `factur-x.xml` embarqué), denrées à 5,5 % et produits d'entretien à 20 % ;
- `FermeTroisChenes_FTC-2026-034.pdf` : facture PDF d'un producteur, sans anomalie ;
- `ClimHotte_CHS-2026-0457.pdf` : facture PDF de maintenance, à laquelle il manque des mentions obligatoires.

### Session 2 : procédures et skills

- `factures/` : les 13 documents du mois de septembre (12 factures et une copie en doublon), dans tous les formats : Factur-X, UBL, PDF, PDF scanné ;
- `historique-prix-aout.csv` : prix d'achat d'août (séparateur point-virgule, virgule décimale, encodage UTF-8 lisible par Excel) ;
- `fiches-techniques/` : cinq plats de la carte ;
- `reglementaire/` : fiches de référence sur les taux de TVA et les mentions obligatoires.

### Session 3 : le dossier Claude Code

`Comptoir-des-Saisons/` est le **dossier de départ** : les sources sont rangées selon la structure présentée en session 1, et le relevé bancaire de septembre est ajouté (`sources/releves-bancaires/septembre-2026.csv`). Il ne contient **ni `CLAUDE.md`, ni skills, ni sous-agents** : les participants les construisent pendant la session.

## Le dossier formateur

- `corrige-anomalies.md` : inventaire complet, anomalies avec leur impact chiffré, variations de prix, coût matière des plats et rapprochement bancaire attendus ;
- `solutions-session-2/` : procédures complétées et skills de la session 2 ;
- `Comptoir-des-Saisons-complet/` : le dossier final entièrement construit (`CLAUDE.md`, `.claude/skills/`, `.claude/agents/`). Il sert à la démonstration « bande-annonce » de la session 1 et de version de secours en session 3.

> Le dossier `.claude` est masqué par défaut sous Windows et macOS : afficher les fichiers cachés pour le voir.

## Notes techniques sur les formats

- Les **Factur-X** sont des PDF construits selon la structure PDF/A-3 (polices embarquées, profil de couleur sRGB, métadonnées XMP Factur-X) avec le fichier `factur-x.xml` au format CII, profil EN 16931, en pièce jointe de type « Data ». Ils n'ont pas été passés dans un validateur officiel (veraPDF, validateur FNFE-MPE) : ils conviennent parfaitement à un usage pédagogique, pas à un test de conformité de logiciel.
- Les **UBL** sont des fichiers XML au format UBL 2.1, profil EN 16931.
- Le fichier XML d'une Factur-X est visible dans la liste des pièces jointes d'Adobe Acrobat Reader (icône trombone).
- Les **PDF scannés** ne contiennent qu'une image : leur texte n'est pas sélectionnable, Claude doit les lire visuellement.
