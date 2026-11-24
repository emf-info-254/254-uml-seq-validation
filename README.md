# 🧩 Module 254 — Évaluation sommative : Diagramme de séquence UML
 
## 🎯 Objectif
Représenter chronologiquement les échanges entre les acteurs et les systèmes d'un processus métier à l'aide d'un diagramme de séquence UML.
 
## 📋 Consignes
Cet exercice est à rendre à votre maître professionnel pour validation.
 
## Contexte
 
La **Pharmacie du Lapin Vert** à Neyruz souhaite documenter son processus de délivrance des médicaments sur ordonnance électronique. Ce processus fait intervenir plusieurs personnes, mais aussi plusieurs systèmes informatiques qui doivent communiquer entre eux : le logiciel de gestion de la pharmacie, le système de la caisse maladie du patient, le système de commande du grossiste et une passerelle d'envoi de SMS.
 
L'objectif est de mieux comprendre **qui communique avec qui, dans quel ordre, et si l'émetteur attend une réponse ou non**.
 
## Acteurs et systèmes impliqués
 
| Élément | Rôle |
|---|---|
| **Patient** | Personne qui vient chercher ses médicaments |
| **Pharmacien** | Collaborateur de la pharmacie au comptoir |
| **PharmaSoft** | Logiciel de gestion de la pharmacie (stock, dossiers patients, facturation) |
| **Système Assureur** | Système informatique de la caisse maladie du patient |
| **Grossiste** | Système de commande en ligne du grossiste en médicaments *PharmaDistri SA* |
| **Passerelle SMS** | Service d'envoi de SMS utilisé par la pharmacie |
 
## Processus métier à **la Pharmacie du Lapin Vert**
 
### 1. Présentation de l'ordonnance
- Le patient remet au pharmacien son ordonnance électronique (QR code) et sa carte d'assuré.
- Le pharmacien scanne le QR code dans PharmaSoft, qui affiche la liste des médicaments prescrits.
### 2. Vérification de la couverture d'assurance
- PharmaSoft interroge le Système Assureur pour vérifier la couverture du patient. **PharmaSoft attend la réponse avant de continuer.**
- Le Système Assureur retourne les conditions de couverture, c'est-à-dire le montant à la charge du patient (quote-part).
### 3. Contrôle du stock
- **Pour chaque médicament** de l'ordonnance, PharmaSoft vérifie lui-même s'il est disponible en stock.
### 4. Validation pharmaceutique
- Le pharmacien lance le contrôle des interactions médicamenteuses. PharmaSoft effectue le contrôle lui-même et affiche le résultat au pharmacien.
- Le pharmacien explique la posologie au patient.
### 5. Paiement
- Le patient paie la quote-part de l'ensemble de l'ordonnance au comptoir.
- Le processus de paiement au comptoir est déjà documenté dans un autre diagramme de séquence nommé **« Paiement au comptoir »**. Il ne doit pas être détaillé ici : représentez-le à l'aide d'un **cadre `ref`**.
### 6. Délivrance des médicaments
La suite dépend de la disponibilité des médicaments :
 
- **Si tous les médicaments sont en stock**, le pharmacien remet les médicaments au patient.
- **Si au moins un médicament n'est pas en stock** :
  1. Le pharmacien remet au patient les médicaments disponibles.
  2. PharmaSoft transmet une commande au Grossiste pour les médicaments manquants. **PharmaSoft n'attend pas de réponse.**
  3. Plus tard, le Grossiste confirme la livraison à PharmaSoft. **Le Grossiste n'attend pas de réponse.**
  4. PharmaSoft demande à la Passerelle SMS d'envoyer un SMS au patient, puis la Passerelle SMS transmet le SMS au patient pour l'informer que ses médicaments l'attendent. **Aucun des deux n'attend de réponse.**
  5. Le patient revient à la pharmacie et le pharmacien lui remet les médicaments restants.
### 7. Facturation à l'assurance
- En fin de journée, PharmaSoft transmet la facture électronique au Système Assureur. **PharmaSoft n'attend pas de réponse.**
## Travail demandé
1. Identifiez les **lignes de vie** (acteurs et systèmes) à représenter.
2. Identifiez les **messages** échangés et leur ordre chronologique.
3. Pour chaque message, déterminez s'il s'agit d'un message **synchrone**, **asynchrone** ou d'un **message de retour**.
4. Représentez le diagramme de séquence en respectant la syntaxe et les symboles définis par la norme UML. Votre diagramme doit contenir :
   - les lignes de vie et les périodes d'activité ;
   - les types de messages corrects (flèche pleine, flèche ouverte, retour en pointillé) ;
   - un fragment **`loop`** pour le contrôle du stock (étape 3) ;
   - un fragment **`alt`** pour la délivrance des médicaments (étape 6) ;
   - un cadre **`ref`** « Paiement au comptoir » (étape 5) ;
   - les messages réflexifs (un système qui s'envoie un message à lui-même) aux étapes 3 et 4.
## 🛠️ Outils (au choix)
 
### Option A — Enterprise Architect
Réalisez le diagramme dans Enterprise Architect, puis exportez-le en image (PNG).
 
### Option B — Mermaid
Écrivez le diagramme en syntaxe Mermaid dans un fichier Markdown, dans un bloc ` ```mermaid `. Vérifiez le rendu avec [Mermaid Live Editor](https://mermaid.live) ou dans VS Code avant de rendre votre travail.
 
Aide-mémoire Mermaid :
 
| Élément UML | Syntaxe Mermaid |
|---|---|
| Acteur | `actor Patient` |
| Système / objet | `participant PharmaSoft` |
| Message synchrone | `A->>B: message` |
| Message asynchrone | `A-)B: message` |
| Message de retour | `B-->>A: réponse` |
| Message réflexif | `A->>A: message` |
| Période d'activité | `activate B` / `deactivate B` (ou `A->>+B` / `B-->>-A`) |
| Alternative | `alt condition` … `else autre condition` … `end` |
| Boucle | `loop condition` … `end` |
| Référence | Mermaid n'a pas de cadre `ref` : utilisez `Note over A,B: ref — Nom du diagramme` |
 
## 📦 Travail à rendre
La convention de nommage du fichier à rendre est **254_sd_NOM** (le nom est en capitales), avec l'extension correspondant à l'outil choisi :
 
- Enterprise Architect : **254_sd_NOM.png**
- Mermaid : **254_sd_NOM.md**
Exemple : **254_sd_DUMAS.md**
 
## 📊 Critères d'évaluation
 
| Critère | Points |
|---|---|
| Toutes les lignes de vie sont présentes et correctement représentées (acteurs / systèmes) | 3 |
| Les messages sont complets et dans le bon ordre chronologique | 5 |
| Les types de messages (synchrone, asynchrone, retour) sont correctement choisis | 4 |
| Le fragment `loop` est correctement utilisé avec sa condition | 2 |
| Le fragment `alt` est correctement utilisé avec ses deux conditions | 2 |
| Le cadre `ref` « Paiement au comptoir » est présent au bon endroit | 1 |
| Les messages réflexifs sont représentés | 1 |
| Les périodes d'activité sont cohérentes | 1 |
| Lisibilité générale et respect de la convention de nommage | 1 |
| **Total** | **20** |
