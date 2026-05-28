**Voici les données à utiliser pour alimenter plus facilement vos workflows.**

## Module 4

#### Étape — Ajouter le nœud "Send Email"

1. Cliquer sur le **"+"** à droite du trigger Gmail
2. Rechercher **"Gmail"** → sélectionner **"Gmail"** (nœud d'action, pas le trigger)
3. Configurer :
   - **Credential** : même credential Gmail
   - **Resource** : Message
   - **Operation** : Send
   - **To** : cliquer sur l'icône **"Expression"** (éclair) → taper `{{ $json.from }}`
   - **Subject** : `RE: {{ $json.subject }}`
   - **Message** :
     ```
     Bonjour,

     Nous avons bien reçu votre devis signé. 
     Nous revenons vers vous très prochainement.

     Cordialement,
     L'équipe
     ```

#### Étape — Configurer la condition

Le nœud IF évalue une condition et oriente le flux vers deux sorties : **"true"** (condition vraie) ou **"false"** (condition fausse).

Configuration :

Dans le *Gmail trigger* activer l'option Download attachments => on observe alors un nouvel objet `Binary` dans lequel il y a des paramétres

- **Value 1** : cliquer sur Expression → `{{ Object.values($binary)[0].fileExtension }}`
- **Operation** : `is equal to` 
- **Value 2** : `pdf` évalue une condition et oriente le flux vers deux sorties : **"true"** (condition vraie) ou **"false"** (condition fausse).

Configuration :

Dans le *Gmail trigger* activer l'option Download attachments => on observe alors un nouvel objet `Binary` dans lequel il y a des paramétres

- **Value 1** : cliquer sur Expression → `{{ Object.values($binary)[0].fileExtension }}`
- **Operation** : `is equal to` 
- **Value 2** : `pdf`

#### Étape — Ajouter le nœud Google Tasks

1. Cliquer sur **"+"** après le nœud Send Email
2. Rechercher **"Google Tasks"** → ajouter
3. Configurer un nouveau **Credential Google** (même procédure OAuth que Gmail)
4. Configuration du nœud :
   - **Resource** : Task
   - **Operation** : Create
   - **Task List** : sélectionner "Mes tâches" (ou en créer une dédiée "Devis à traiter")
   - **Title** : `Suivi devis - {{ $('Gmail Trigger').item.json.from }}`
   - **Notes** : `Devis signé reçu le {{ $now.format('dd/MM/yyyy') }} - Objet : {{ $('Gmail Trigger').item.json.subject }}`
   - **Due Date** : (optionnel) `{{ $now.plus(3, 'days').toISO() }}`

#### Étape — Ajouter la notification interne

1. Cliquer sur **"+"** après Google Tasks
2. Rechercher **"Gmail"** → ajouter un nœud Send
3. Configuration :
   - **To** : votre propre adresse email (en dur, pas dynamique)
   - **Subject** : `Nouveau devis signé reçu`
   - **Message** :
     ```
     Un devis signé vient d'être reçu.

     De : {{ $('Gmail Trigger').item.json.from }}
     Objet : {{ $('Gmail Trigger').item.json.subject }}
     Reçu le : {{ $now.format('dd/MM/yyyy à HH:mm') }}

     Une tâche de suivi a été créée dans Google Tasks.
     ```

## Module 5

{{ $('Gmail Trigger').item.binary[Object.keys($('Gmail Trigger').item.binary)[0]].fileName }}

{{ $('Gmail Trigger').item.binary[Object.keys($('Gmail Trigger').item.binary)[0]] }}

Pour Virginie : {{ $('Gmail Trigger').item.binary[Object.keys($('Gmail Trigger').item.binary)[0]].fileExtension }}



## Module 6

{{ Object.keys($('Gmail Trigger').item.binary)[0] }}


### Ajouter le nœud "Basic LLM Chain" ou "AI Agent"

> ! *Pour ce cas d'usage, on utilise le nœud **"Basic LLM Chain"** — c'est la forme la plus simple d'intégration LLM dans n8n : on envoie un prompt, on reçoit une réponse. On verra la différence avec un vrai "AI Agent" en fin de module.*

1. Rechercher **"Basic LLM Chain"** → ajouter
2. Dans le nœud, cliquer sur **"Add model"** → sélectionner **"Google Gemini Chat Model"**
3. Configurer le modèle :
   - **Credential** : credential Gemini créé
   - **Model** : `gemini-1.5-flash` (bon équilibre vitesse/qualité)

### Configurer le prompt système

Le **prompt système** définit le rôle et le comportement de l'IA. C'est l'équivalent des instructions permanentes.

```
Tu es un assistant pour une petite entreprise de services. 
Tu analyses des documents PDF de devis signés envoyés par des clients.

Ton travail est de :
1. Vérifier que le document est bien un devis signé (et non une facture, un contrat ou autre chose)
2. Si c'est bien un devis signé, extraire les informations clés : nom du client, montant total, objet de la prestation
3. Rédiger un email de confirmation chaleureux et professionnel en français, personnalisé avec ces informations

Réponds UNIQUEMENT en JSON valide, sans aucun texte avant ou après, avec cette structure exacte :
{
  "est_un_devis": true ou false,
  "client_nom": "nom du client ou null",
  "montant": "montant total ou null",
  "prestation": "description courte de la prestation ou null",
  "email_sujet": "objet de l'email de réponse",
  "email_corps": "corps complet de l'email de réponse"
}
```

### Configurer le prompt utilisateur

Le **prompt utilisateur** contient les données dynamiques — ici, le contenu du PDF.

```
Voici le contenu du document PDF reçu par email :

---
{{ $('Extract from File').item.json.text }}
---

Expéditeur de l'email : {{ $('Gmail Trigger').item.json.from }}
Objet de l'email : {{ $('Gmail Trigger').item.json.subject }}

Analyse ce document et fournis ta réponse JSON.
```

### Script formateur — L'art du prompt
> *"Ce qu'on vient d'écrire s'appelle un 'prompt'. C'est l'instruction qu'on donne à l'IA. Remarquez trois choses importantes : on lui a donné un rôle précis, on lui a dit exactement quoi faire étape par étape, et on lui a demandé un format de sortie JSON très strict. Ce dernier point est crucial : si l'IA répond en prose libre, on ne peut pas utiliser sa réponse dans le workflow. En lui imposant du JSON, on peut brancher sa réponse sur des nœuds suivants comme n'importe quelle autre donnée."*

---

## Étape 3 — Parser la réponse JSON de Gemini (10 min)

La réponse de Gemini arrive comme une chaîne de texte. On doit la convertir en objet JSON exploitable.

### Ajouter le nœud "Code"
1. Rechercher **"Code"** → ajouter
2. **Language** : JavaScript
3. Code :
```javascript
const responseText = $input.item.json.text;

// Nettoyer la réponse (Gemini peut parfois ajouter des backticks)
const cleaned = responseText
  .replace(/```json/g, '')
  .replace(/```/g, '')
  .trim();

const parsed = JSON.parse(cleaned);

return { json: parsed };
```
