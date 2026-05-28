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

## Module 6

