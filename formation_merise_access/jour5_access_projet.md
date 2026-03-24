# Jour 5 - Maîtrise de MS Access et Projet Final

## Durée : 6 heures

---

## Planning de la Journée

### Matinée (9h00 - 12h00) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 9h00 - 9h15 | Révision Jour 4 | Rappel Tables Access, Questions/Réponses | 15min |
| 9h15 - 11h00 | MS Access - Relations | Création relations, Intégrité référentielle | 1h45 |
| 11h00 - 11h15 | PAUSE CAFÉ | | 15min |
| 11h15 - 12h00 | MS Access - Requêtes Partie 1 | Introduction, Requêtes simples | 45min |

### Après-midi (13h30 - 16h30) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 13h30 - 14h30 | MS Access - Requêtes Partie 2 | Critères, Jointures, Paramètres | 1h |
| 14h30 - 15h30 | MS Access - Requêtes Partie 3 | Requêtes Action, SQL | 1h |
| 15h30 - 15h45 | PAUSE | | 15min |
| 15h45 - 16h15 | Projet Pratique Final | Application complète Merise/Access | 30min |
| 16h15 - 16h30 | Évaluation et Clôture | Bilan, Attestations | 15min |

---

## Module 1 : Révision Jour 4 (15 min)

### Quiz de Révision

1. Quels sont les types de données disponibles dans Access ?
2. Comment définit-on une clé primaire en mode création ?
3. À quoi sert un masque de saisie ?
4. Comment importe-t-on des données depuis Excel ?

### Points de Clarification

Discussion sur les difficultés rencontrées lors des exercices du Jour 4.

---

## Module 2 : MS Access - Relations (1h45)

### 2.1 Création de Relations entre Tables

#### Accès à la Fenêtre Relations

```
Outils de base de données → Relations
```

#### Interface des Relations

```
┌─────────────────────────────────────────────────────────────────┐
│  Création  Outils de relation                                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌──────────────┐          ┌──────────────┐                    │
│   │  tblClient   │          │ tblCommande  │                    │
│   ├──────────────┤          ├──────────────┤                    │
│   │ NumClient    │──────────│ NumCommande  │                    │
│   │ NomClient    │    1:∞   │ DateCommande │                    │
│   │ Email        │          │ NumClient    │                    │
│   └──────────────┘          └──────────────┘                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Étapes de Création d'une Relation

1. **Ouvrir la fenêtre Relations**
2. **Ajouter les tables** (clic droit → Afficher la table)
3. **Glisser-déposer** la clé primaire vers la clé étrangère
4. **Configurer la relation** dans la boîte de dialogue
5. **Valider** la relation

### 2.2 Types de Relations

#### Relation Un à Plusieurs (1:N)

**La plus courante** : Un enregistrement d'une table est lié à plusieurs enregistrements d'une autre table.

```
CLIENT (1) ────────── (N) COMMANDE
Un client peut avoir plusieurs commandes
Une commande appartient à un seul client
```

#### Relation Un à Un (1:1)

**Rare** : Un enregistrement d'une table est lié à exactement un enregistrement d'une autre table.

```
EMPLOYE (1) ────────── (1) DETAIL_EMPLOYE
Un employé a un seul détail
Un détail appartient à un seul employé
```

#### Relation Plusieurs à Plusieurs (N:N)

**Nécessite une table intermédiaire** : Plusieurs enregistrements d'une table peuvent être liés à plusieurs enregistrements d'une autre table.

```
ETUDIANT (N) ────── INSCRIPTION ────── (N) COURS

Décomposition :
ETUDIANT (1) ── (N) INSCRIPTION (N) ── (1) COURS
```

### 2.3 Intégrité Référentielle

#### Définition

L'**intégrité référentielle** garantit la cohérence des relations entre tables. Elle empêche :
- L'ajout d'un enregistrement enfant sans parent
- La suppression d'un parent ayant des enfants
- La modification incohérente des clés

#### Activation

Dans la boîte de dialogue "Modifier les relations" :
- ☑ **Appliquer l'intégrité référentielle**

#### Options de Mise en Cascade

| Option | Description |
|--------|-------------|
| **Mettre à jour en cascade les champs correspondants** | Si la clé primaire change, les FK sont mises à jour |
| **Effacer en cascade les enregistrements correspondants** | Si le parent est supprimé, les enfants aussi |

⚠️ **Attention** : La suppression en cascade peut être dangereuse !

### 2.4 Configuration Complète

#### Démonstration : Schéma Relationnel Complet

Création des relations pour une base commerciale :

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  tblClient   │     │ tblCommande  │     │ tblLigneCom  │
├──────────────┤     ├──────────────┤     ├──────────────┤
│ NumClient    │─┐   │ NumCommande  │─┐   │ NumCommande  │
│ NomClient    │ │   │ DateCommande │ │   │ RefProduit   │
│ Email        │ │   │ NumClient    │◄┘   │ Quantite     │
└──────────────┘ │   │ Statut       │     │ PrixUnitaire │
                 │   └──────────────┘     └──────────────┘
                 │          1:∞                   ↑
                 │                                │
                 └────────────────────────────────┼───┐
                              1:∞                 │   │
                                                  │   │
                           ┌──────────────────────┘   │
                           │                          │
                   ┌───────┴──────┐                   │
                   │  tblProduit  │                   │
                   ├──────────────┤                   │
                   │ RefProduit   │───────────────────┘
                   │ Designation  │         1:∞
                   │ PrixUnitaire │
                   │ Stock        │
                   └──────────────┘
```

### Activité 5.1 : Création de Relations
**Durée : 25 minutes**

Dans votre base "GestionCommerciale" :

1. **Créer les tables manquantes** :
   - tblClient (NumClient, NomClient, Email, Telephone)
   - tblCommande (NumCommande, DateCommande, NumClient)
   - tblLigneCommande (NumCommande, RefProduit, Quantite)

2. **Établir les relations** :
   - tblClient → tblCommande (1:N)
   - tblCommande → tblLigneCommande (1:N)
   - tblProduit → tblLigneCommande (1:N)

3. **Activer l'intégrité référentielle** avec mise à jour en cascade

---

## Module 3 : MS Access - Requêtes Partie 1 (45 min)

### 3.1 Introduction aux Requêtes

#### Définition

Une **requête** permet d'interroger, filtrer, trier et manipuler les données d'une ou plusieurs tables.

#### Types de Requêtes

| Type | Fonction |
|------|----------|
| **Sélection** | Afficher des données filtrées |
| **Analyse croisée** | Résumer des données |
| **Création de table** | Créer une table à partir de données |
| **Ajout** | Ajouter des enregistrements |
| **Mise à jour** | Modifier des enregistrements |
| **Suppression** | Supprimer des enregistrements |

### 3.2 Requêtes de Sélection Simples

#### Mode Création

```
Créer → Création de requête
```

#### Interface de Création

```
┌─────────────────────────────────────────────────────────────────┐
│                    ZONE DES TABLES                              │
│   ┌──────────────┐     ┌──────────────┐                         │
│   │  tblProduit  │     │              │                         │
│   ├──────────────┤     │              │                         │
│   │ RefProduit   │     │              │                         │
│   │ Designation  │     │              │                         │
│   │ PrixUnitaire │     │              │                         │
│   └──────────────┘     └──────────────┘                         │
├─────────────────────────────────────────────────────────────────┤
│                    GRILLE DE REQUÊTE                            │
│ ┌──────────────┬──────────────┬──────────────┬────────────────┐ │
│ │ Champ:       │ RefProduit   │ Designation  │ PrixUnitaire   │ │
│ │ Table:       │ tblProduit   │ tblProduit   │ tblProduit     │ │
│ │ Tri:         │              │ Croissant    │                │ │
│ │ Afficher:    │ ☑            │ ☑            │ ☑              │ │
│ │ Critères:    │              │              │ >100           │ │
│ │ Ou:          │              │              │                │ │
│ └──────────────┴──────────────┴──────────────┴────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

#### Composants de la Grille

| Ligne | Fonction |
|-------|----------|
| Champ | Champ à inclure |
| Table | Table source |
| Tri | Croissant, Décroissant ou aucun |
| Afficher | Afficher ou masquer le champ |
| Critères | Condition de filtrage |
| Ou | Conditions alternatives |

### 3.3 Assistant Requête

#### Utilisation de l'Assistant

1. **Créer** → **Assistant Requête**
2. Choisir le type de requête
3. Sélectionner les tables et champs
4. Configurer les options
5. Nommer et exécuter

#### Types d'Assistants

- Assistant Requête simple
- Assistant Requête analyse croisée
- Assistant Recherche de doublons
- Assistant Recherche de non-correspondance

### 3.4 Exemples de Requêtes Simples

#### Requête 1 : Tous les produits

```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit;
```

#### Requête 2 : Produits triés par prix

```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
ORDER BY PrixUnitaire DESC;
```

#### Requête 3 : Produits chers (> 100€)

```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
WHERE PrixUnitaire > 100;
```

### Activité 5.2 : Requêtes Simples
**Durée : 20 minutes**

Créez les requêtes suivantes :

1. **qryTousProduits** : Liste de tous les produits
2. **qryProduitsAlerte** : Produits dont le stock < seuil d'alerte
3. **qryProduitsTriPrix** : Produits triés par prix décroissant
4. **qryClientsAlpha** : Clients triés par nom

---

## Module 4 : MS Access - Requêtes Partie 2 (1h)

### 4.1 Requêtes avec Critères

#### Opérateurs de Comparaison

| Opérateur | Signification | Exemple |
|-----------|---------------|---------|
| = | Égal | ="Paris" |
| <> | Différent | <>"Annulé" |
| > | Supérieur | >100 |
| < | Inférieur | <50 |
| >= | Supérieur ou égal | >=10 |
| <= | Inférieur ou égal | <=1000 |
| Between...And | Intervalle | Between 10 And 100 |
| Like | Correspondance | Like "A*" |
| In | Liste | In("Paris","Lyon") |
| Is Null | Valeur nulle | Is Null |
| Is Not Null | Non null | Is Not Null |

#### Caractères Joker pour LIKE

| Caractère | Signification | Exemple |
|-----------|---------------|---------|
| * | Plusieurs caractères | Like "A*" → Abcd, Azerty |
| ? | Un seul caractère | Like "A?" → Ab, Ac |
| # | Un chiffre | Like "A#" → A1, A9 |
| [abc] | Un caractère parmi | Like "[ABC]*" |
| [!abc] | Un caractère sauf | Like "[!ABC]*" |
| [-] | Plage de caractères | Like "[A-Z]*" |

#### Exemples Pratiques

```
Critère sur NomClient : Like "Dup*"
→ Dupont, Dupuis, Durand (ne correspond pas)

Critère sur CodePostal : Like "75*"
→ Tous les codes postaux de Paris

Critère sur DateCommande : Between #01/01/2024# And #31/12/2024#
→ Commandes de l'année 2024
```

### 4.2 Requêtes Multi-Tables (Jointures)

#### Jointure Interne (INNER JOIN)

Affiche uniquement les enregistrements correspondants dans les deux tables.

```
┌──────────────┐     ┌──────────────┐
│  tblClient   │─────│ tblCommande  │
│ NumClient    │  =  │ NumClient    │
└──────────────┘     └──────────────┘
```

**SQL** :
```sql
SELECT tblClient.NomClient, tblCommande.NumCommande, tblCommande.DateCommande
FROM tblClient INNER JOIN tblCommande 
ON tblClient.NumClient = tblCommande.NumClient;
```

#### Jointure Externe Gauche (LEFT JOIN)

Affiche tous les enregistrements de la table gauche, même sans correspondance.

```sql
SELECT tblClient.NomClient, tblCommande.NumCommande
FROM tblClient LEFT JOIN tblCommande 
ON tblClient.NumClient = tblCommande.NumClient;
```

*Affiche tous les clients, même ceux sans commande.*

#### Configuration dans Access

1. Double-cliquer sur la ligne de jointure
2. Choisir le type de jointure :
   - Option 1 : Jointure interne
   - Option 2 : Jointure gauche
   - Option 3 : Jointure droite

### 4.3 Requêtes Paramétrées

#### Définition

Une requête **paramétrée** demande une valeur à l'utilisateur lors de l'exécution.

#### Syntaxe

Utiliser des crochets [ ] dans les critères :

```
Critère : [Entrez le nom du client]
```

#### Exemple Complet

**Requête** : Commandes d'un client spécifique

```sql
SELECT tblClient.NomClient, tblCommande.NumCommande, tblCommande.DateCommande
FROM tblClient INNER JOIN tblCommande 
ON tblClient.NumClient = tblCommande.NumClient
WHERE tblClient.NomClient = [Entrez le nom du client];
```

#### Paramètres avec Dates

```sql
SELECT *
FROM tblCommande
WHERE DateCommande BETWEEN [Date début] AND [Date fin];
```

### 4.4 Champs Calculés

#### Syntaxe

```
NomChampCalculé: Expression
```

#### Exemples

**Calcul de montant** :
```
MontantLigne: [Quantite]*[PrixUnitaire]
```

**Concaténation** :
```
NomComplet: [NomClient] & " " & [PrenomClient]
```

**Fonctions de date** :
```
AnneeCommande: Year([DateCommande])
Anciennete: DateDiff("yyyy",[DateInscription],Date())
```

**Condition (IIf)** :
```
Statut: IIf([Stock]<[SeuilAlerte],"Alerte","OK")
```

### Activité 5.3 : Requêtes Avancées
**Durée : 25 minutes**

Créez les requêtes suivantes :

1. **qryCommandesClient** : Commandes d'un client (paramétré)
2. **qryCommandesPeriode** : Commandes entre deux dates (paramétré)
3. **qryMontantLignes** : Lignes de commande avec montant calculé
4. **qryClientsCommandes** : Clients avec leurs commandes (jointure)
5. **qryClientsSansCommande** : Clients n'ayant pas commandé (jointure externe)

---

## Module 5 : MS Access - Requêtes Partie 3 (1h)

### 5.1 Requêtes Action

#### Types de Requêtes Action

| Type | Fonction | Risque |
|------|----------|--------|
| Création de table | Crée une nouvelle table | Faible |
| Ajout | Ajoute des enregistrements | Moyen |
| Mise à jour | Modifie des enregistrements | Élevé |
| Suppression | Supprime des enregistrements | Très élevé |

⚠️ **Attention** : Les requêtes action modifient définitivement les données !

#### Requête de Mise à Jour

**Objectif** : Augmenter les prix de 10%

```sql
UPDATE tblProduit
SET PrixUnitaire = [PrixUnitaire] * 1.1;
```

**En mode création** :
1. Créer une requête de sélection
2. Menu Créer → Mise à jour
3. Ajouter la ligne "Mise à jour" dans la grille
4. Entrer l'expression : [PrixUnitaire]*1.1

#### Requête d'Ajout

**Objectif** : Copier des produits vers une table d'archive

```sql
INSERT INTO tblProduitArchive (RefProduit, Designation, PrixUnitaire)
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
WHERE Stock = 0;
```

#### Requête de Suppression

**Objectif** : Supprimer les produits à stock nul

```sql
DELETE FROM tblProduit
WHERE Stock = 0;
```

⚠️ **Toujours prévisualiser** avant d'exécuter !

### 5.2 Requêtes d'Analyse Croisée

#### Définition

Une requête **d'analyse croisée** résume les données sous forme de tableau croisé (type tableau croisé dynamique).

#### Structure

```
┌───────────────┬─────────┬─────────┬─────────┬─────────┐
│               │ Janv.   │ Févr.   │ Mars    │ Total   │
├───────────────┼─────────┼─────────┼─────────┼─────────┤
│ Produit A     │ 150     │ 200     │ 180     │ 530     │
│ Produit B     │ 80      │ 120     │ 95      │ 295     │
│ Produit C     │ 300     │ 280     │ 350     │ 930     │
└───────────────┴─────────┴─────────┴─────────┴─────────┘
```

#### Syntaxe SQL

```sql
TRANSFORM Sum([Quantite]) AS SommeDeQuantite
SELECT RefProduit
FROM tblLigneCommande
GROUP BY RefProduit
PIVOT Format([DateCommande],"mmmm");
```

### 5.3 Introduction au SQL

#### Mode SQL dans Access

```
Affichage → Mode SQL
```

#### Structure d'une Requête SELECT

```sql
SELECT champ1, champ2, ...
FROM table1 [JOIN table2 ON condition]
WHERE condition
GROUP BY champ
HAVING condition_groupe
ORDER BY champ [ASC|DESC];
```

#### Exemples SQL

**Sélection simple** :
```sql
SELECT * FROM tblClient;
```

**Avec filtre et tri** :
```sql
SELECT NomClient, Email
FROM tblClient
WHERE Ville = 'Paris'
ORDER BY NomClient;
```

**Avec jointure** :
```sql
SELECT c.NomClient, cmd.NumCommande, cmd.DateCommande
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
WHERE cmd.DateCommande >= #01/01/2024#;
```

**Avec agrégation** :
```sql
SELECT NumClient, COUNT(*) AS NbCommandes, SUM(Montant) AS TotalAchats
FROM tblCommande
GROUP BY NumClient
HAVING COUNT(*) > 5;
```

### 5.4 Fonctions SQL Utiles

#### Fonctions d'Agrégation

| Fonction | Description |
|----------|-------------|
| COUNT(*) | Nombre d'enregistrements |
| SUM(champ) | Somme des valeurs |
| AVG(champ) | Moyenne des valeurs |
| MIN(champ) | Valeur minimale |
| MAX(champ) | Valeur maximale |

#### Fonctions de Texte

| Fonction | Description |
|----------|-------------|
| Left(texte, n) | n premiers caractères |
| Right(texte, n) | n derniers caractères |
| Mid(texte, pos, n) | n caractères à partir de pos |
| Len(texte) | Longueur du texte |
| UCase(texte) | Majuscules |
| LCase(texte) | Minuscules |

#### Fonctions de Date

| Fonction | Description |
|----------|-------------|
| Date() | Date du jour |
| Now() | Date et heure actuelles |
| Year(date) | Année |
| Month(date) | Mois |
| Day(date) | Jour |
| DateAdd(intervalle, n, date) | Ajouter à une date |
| DateDiff(intervalle, date1, date2) | Différence entre dates |

### Activité 5.4 : Requêtes Action et SQL
**Durée : 20 minutes**

1. **Requête mise à jour** : Augmenter de 5% les produits de la catégorie "Électronique"
2. **Requête suppression** : Supprimer les commandes antérieures à 2020
3. **Mode SQL** : Écrire une requête affichant le CA par client

---

## Module 6 : Projet Pratique Final (30 min)

### 6.1 Énoncé du Projet

#### Contexte

Vous devez concevoir et implémenter une base de données pour une **librairie scolaire** qui gère :
- Les livres (références, titres, auteurs, éditeurs, prix)
- Les clients (élèves et professeurs)
- Les commandes et ventes
- Le stock

#### Travail Demandé

**Phase 1 : Conception Merise (10 min)**
1. Identifier les entités et attributs
2. Créer le MCD avec les cardinalités
3. Transformer en MLD

**Phase 2 : Implémentation Access (15 min)**
1. Créer les tables
2. Définir les relations
3. Saisir quelques données de test
4. Créer 2-3 requêtes utiles

**Phase 3 : Présentation (5 min)**
- Montrer le schéma relationnel
- Démontrer les requêtes

### 6.2 Modèle Attendu

#### MCD Simplifié

```
┌──────────────┐       ┌──────────────┐       ┌──────────────┐
│    AUTEUR    │       │    LIVRE     │       │   EDITEUR    │
├──────────────┤  0,n  ├──────────────┤  0,n  ├──────────────┤
│ CodeAuteur   │───────│ ISBN         │───────│ CodeEditeur  │
│ NomAuteur    │ ecrit │ Titre        │publie │ NomEditeur   │
│ PrenomAuteur │  1,n  │ PrixVente    │  1,n  │              │
└──────────────┘       │ Stock        │       └──────────────┘
                       └──────┬───────┘
                              │
                         0,n  │ contient
                              │ Quantite
                       ┌──────┴───────┐
                       │   COMMANDE   │
                       ├──────────────┤
                       │ NumCommande  │
                       │ DateCommande │
                       │ Statut       │
                       └──────┬───────┘
                              │
                         1,1  │ passe
                              │
                       ┌──────┴───────┐
                       │    CLIENT    │
                       ├──────────────┤
                       │ NumClient    │
                       │ NomClient    │
                       │ TypeClient   │
                       │ Email        │
                       └──────────────┘
```

#### MLD

```
AUTEUR (CodeAuteur, NomAuteur, PrenomAuteur)
EDITEUR (CodeEditeur, NomEditeur)
LIVRE (ISBN, Titre, PrixVente, Stock, #CodeEditeur)
ECRIT (#CodeAuteur, #ISBN)
CLIENT (NumClient, NomClient, TypeClient, Email)
COMMANDE (NumCommande, DateCommande, Statut, #NumClient)
LIGNE_COMMANDE (#NumCommande, #ISBN, Quantite)
```

---

## Module 7 : Évaluation et Clôture (15 min)

### 7.1 Bilan de la Formation

#### Compétences Acquises

- ✅ Comprendre et appliquer la méthode Merise
- ✅ Créer des modèles E/A, MCD, MLD, MPD
- ✅ Concevoir et implémenter une base de données Access
- ✅ Créer et gérer des tables et relations
- ✅ Écrire des requêtes simples et avancées

#### Points Forts et Axes d'Amélioration

Discussion ouverte sur :
- Ce qui a bien fonctionné
- Ce qui pourrait être amélioré
- Les besoins de formation complémentaire

### 7.2 Évaluation des Acquis

#### Questionnaire d'Auto-Évaluation

1. Je sais identifier les entités et attributs d'un système : ☐1 ☐2 ☐3 ☐4 ☐5
2. Je sais créer un MCD avec les cardinalités : ☐1 ☐2 ☐3 ☐4 ☐5
3. Je sais transformer un MCD en MLD : ☐1 ☐2 ☐3 ☐4 ☐5
4. Je sais créer des tables dans Access : ☐1 ☐2 ☐3 ☐4 ☐5
5. Je sais établir des relations avec intégrité référentielle : ☐1 ☐2 ☐3 ☐4 ☐5
6. Je sais créer des requêtes de sélection : ☐1 ☐2 ☐3 ☐4 ☐5
7. Je me sens capable d'utiliser ces outils avec mes élèves : ☐1 ☐2 ☐3 ☐4 ☐5

### 7.3 Questionnaire de Satisfaction

- Contenu de la formation
- Qualité pédagogique
- Organisation matérielle
- Applicabilité professionnelle
- Suggestions d'amélioration

### 7.4 Perspectives d'Utilisation Pédagogique

#### Applications en Classe

1. **Projets de gestion** : Créer une base de données pour un cas d'entreprise
2. **Travaux pratiques** : Exercices de modélisation
3. **Évaluations** : Questions sur Merise et Access
4. **Projets transversaux** : Collaboration avec d'autres matières

#### Ressources Complémentaires

- Documentation officielle Microsoft Access
- Tutoriels vidéo recommandés
- Forums et communautés d'entraide
- Bibliographie sur Merise

### 7.5 Remise des Attestations

Chaque participant reçoit une **attestation de formation** mentionnant :
- Intitulé de la formation
- Durée (30 heures)
- Compétences validées
- Date et signature

---

## Synthèse Générale de la Formation

### Les 5 Jours en Résumé

| Jour | Thème Principal | Compétences Clés |
|------|-----------------|------------------|
| 1 | Introduction Merise | Entités, Attributs, Relations E/A |
| 2 | MCT et MCD | Traitements, Normalisation, MCD complet |
| 3 | MLD | Transformation MCD→MLD, Clés |
| 4 | MPD et Access | Types, Contraintes, Tables Access |
| 5 | Access Avancé | Relations, Requêtes, Projet |

### Feuille de Route Post-Formation

1. **Semaine 1** : Réviser les supports et refaire les exercices
2. **Semaine 2** : Créer un projet personnel avec Merise et Access
3. **Mois 1** : Préparer une séquence pédagogique pour les élèves
4. **Trimestre 1** : Mettre en œuvre avec les élèves et partager les retours

---

## Ressources Complémentaires

- [Exercices supplémentaires - Jour 5](./activites/exercices_jour5.md)
- [Corrigés des exercices](./corriges/corriges_jour5.md)
- [Projet final - Corrigé](./corriges/projet_final_corrige.md)
- [Ressources pédagogiques](./ressources/)
