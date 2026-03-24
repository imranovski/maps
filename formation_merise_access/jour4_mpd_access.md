# Jour 4 - MPD et Introduction à MS Access

## Durée : 6 heures

---

## Planning de la Journée

### Matinée (9h00 - 12h00) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 9h00 - 9h15 | Révision Jour 3 | Rappel MLD, Questions/Réponses | 15min |
| 9h15 - 10h15 | Modèle MPD | Implémentation physique, Types, Index | 1h |
| 10h15 - 10h30 | PAUSE CAFÉ | | 15min |
| 10h30 - 12h00 | MS Access - Introduction | Interface, Création BDD, Bonnes pratiques | 1h30 |

### Après-midi (13h30 - 16h30) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 13h30 - 14h45 | MS Access - Tables Partie 1 | Création tables, Types de données, Clés | 1h15 |
| 14h45 - 15h00 | PAUSE | | 15min |
| 15h00 - 16h30 | MS Access - Tables Partie 2 | Saisie, Validation, Import/Export | 1h30 |

---

## Module 1 : Révision Jour 3 (15 min)

### Quiz de Révision

1. Comment transforme-t-on une relation 1:N en MLD ?
2. Qu'est-ce qu'une table associative ?
3. Où migre la clé étrangère dans une relation 1:1 ?
4. Comment gère-t-on une relation ternaire en MLD ?

### Points de Clarification

Discussion sur les difficultés rencontrées lors des exercices du Jour 3.

---

## Module 2 : Modèle Physique de Données (MPD) (1h)

### 2.1 Introduction au MPD

#### Définition

Le **Modèle Physique de Données (MPD)** est l'implémentation concrète du MLD dans un SGBD spécifique. Il prend en compte les caractéristiques techniques du système cible.

#### Objectif

Traduire le MLD en **instructions SQL** ou en structure de base de données réelle.

### 2.2 Du MLD au MPD

#### Étapes de Transformation

1. **Choix du SGBD** : MS Access, MySQL, Oracle, etc.
2. **Définition des types de données** selon le SGBD
3. **Création des contraintes** : NOT NULL, UNIQUE, CHECK
4. **Définition des index** pour les performances
5. **Implémentation des relations** : clés étrangères

### 2.3 Types de Données

#### Types de Données Courants

| Type Générique | MS Access | MySQL | Description |
|----------------|-----------|-------|-------------|
| Entier | Entier long | INT | Nombres entiers |
| Décimal | Réel double | DECIMAL | Nombres à virgule |
| Texte court | Texte court (255) | VARCHAR | Chaînes limitées |
| Texte long | Mémo | TEXT | Chaînes longues |
| Date | Date/Heure | DATE | Dates |
| Date et heure | Date/Heure | DATETIME | Dates et heures |
| Booléen | Oui/Non | BOOLEAN | Vrai/Faux |
| Image | Objet OLE | BLOB | Fichiers binaires |
| Auto-incrément | NuméroAuto | AUTO_INCREMENT | Clé auto |

#### Choix du Type Approprié

**Règles générales** :
- **Numéros d'identification** : NuméroAuto (auto-incrément)
- **Codes fixes** : Texte court avec taille définie
- **Noms, adresses** : Texte court (50-255 caractères)
- **Descriptions** : Mémo/Texte long
- **Prix** : Monétaire ou Réel
- **Quantités** : Entier
- **Dates** : Date/Heure

### 2.4 Contraintes d'Intégrité

#### Types de Contraintes

| Contrainte | Description | Exemple |
|------------|-------------|---------|
| NOT NULL | Valeur obligatoire | Nom NOT NULL |
| UNIQUE | Valeur unique | Email UNIQUE |
| PRIMARY KEY | Clé primaire | NumClient PRIMARY KEY |
| FOREIGN KEY | Clé étrangère | REFERENCES Client(NumClient) |
| CHECK | Condition de validation | CHECK (Prix > 0) |
| DEFAULT | Valeur par défaut | DEFAULT 0 |

#### Exemple de Définition

```sql
CREATE TABLE PRODUIT (
    RefProduit TEXT(10) PRIMARY KEY,
    Designation TEXT(100) NOT NULL,
    PrixUnitaire CURRENCY NOT NULL CHECK (PrixUnitaire > 0),
    Stock INTEGER DEFAULT 0,
    DateCreation DATE DEFAULT Date(),
    Actif YESNO DEFAULT TRUE
);
```

### 2.5 Index et Performances

#### Définition

Un **index** est une structure de données qui accélère la recherche dans une table, comme l'index d'un livre.

#### Quand Créer un Index ?

- ✅ Clés primaires (créé automatiquement)
- ✅ Clés étrangères
- ✅ Colonnes fréquemment utilisées dans les recherches (WHERE)
- ✅ Colonnes utilisées dans les tris (ORDER BY)
- ❌ Colonnes rarement consultées
- ❌ Tables très petites

#### Types d'Index

1. **Index simple** : Sur une seule colonne
2. **Index composite** : Sur plusieurs colonnes
3. **Index unique** : Garantit l'unicité des valeurs

### 2.6 Exemple de MPD Complet

#### MLD de Départ

```
CLIENT (NumClient, NomClient, Email, DateInscription)
COMMANDE (NumCommande, DateCommande, Statut, #NumClient)
PRODUIT (RefProduit, Designation, PrixUnitaire, Stock)
LIGNE_COMMANDE (#NumCommande, #RefProduit, Quantite)
```

#### MPD pour MS Access

```
TABLE CLIENT
─────────────────────────────────────────────────────────────
| Champ           | Type           | Contraintes            |
|─────────────────|────────────────|────────────────────────|
| NumClient       | NuméroAuto     | Clé primaire           |
| NomClient       | Texte(100)     | Obligatoire            |
| Email           | Texte(100)     | Unique                 |
| DateInscription | Date/Heure     | Par défaut: Date()     |
─────────────────────────────────────────────────────────────

TABLE COMMANDE
─────────────────────────────────────────────────────────────
| Champ           | Type           | Contraintes            |
|─────────────────|────────────────|────────────────────────|
| NumCommande     | NuméroAuto     | Clé primaire           |
| DateCommande    | Date/Heure     | Obligatoire, défaut    |
| Statut          | Texte(20)      | Valeur liste           |
| NumClient       | Entier long    | Clé étrangère CLIENT   |
─────────────────────────────────────────────────────────────

TABLE PRODUIT
─────────────────────────────────────────────────────────────
| Champ           | Type           | Contraintes            |
|─────────────────|────────────────|────────────────────────|
| RefProduit      | Texte(10)      | Clé primaire           |
| Designation     | Texte(100)     | Obligatoire            |
| PrixUnitaire    | Monétaire      | Obligatoire, > 0       |
| Stock           | Entier         | Par défaut: 0          |
─────────────────────────────────────────────────────────────

TABLE LIGNE_COMMANDE
─────────────────────────────────────────────────────────────
| Champ           | Type           | Contraintes            |
|─────────────────|────────────────|────────────────────────|
| NumCommande     | Entier long    | Clé primaire, FK       |
| RefProduit      | Texte(10)      | Clé primaire, FK       |
| Quantite        | Entier         | Obligatoire, > 0       |
─────────────────────────────────────────────────────────────
```

### Activité 4.1 : Création d'un MPD
**Durée : 20 minutes**

Transformez le MLD suivant en MPD pour MS Access :

```
ETUDIANT (NumEtud, Nom, Prenom, DateNaissance, Email)
CLASSE (CodeClasse, NomClasse, Niveau, Annee)
APPARTIENT (#NumEtud, #CodeClasse, DateAffectation)
```

---

## Module 3 : MS Access - Introduction et Bases de Données (1h30)

### 3.1 Présentation de l'Interface MS Access

#### Composants Principaux

```
┌─────────────────────────────────────────────────────────────────┐
│  Fichier  Accueil  Créer  Données externes  Outils base données│
├──────────────┬──────────────────────────────────────────────────┤
│              │                                                  │
│   VOLET DE   │           ZONE DE TRAVAIL                        │
│  NAVIGATION  │                                                  │
│              │  ┌────────────────────────────────────────────┐  │
│  □ Tables    │  │                                            │  │
│  □ Requêtes  │  │     Contenu affiché selon l'objet         │  │
│  □ Formulaires│  │     sélectionné (table, requête, etc.)    │  │
│  □ États     │  │                                            │  │
│  □ Macros    │  │                                            │  │
│  □ Modules   │  └────────────────────────────────────────────┘  │
│              │                                                  │
└──────────────┴──────────────────────────────────────────────────┘
```

#### Les Objets d'une Base Access

| Objet | Fonction | Icône |
|-------|----------|-------|
| **Tables** | Stockage des données | 📊 |
| **Requêtes** | Interrogation et manipulation | ❓ |
| **Formulaires** | Saisie et affichage | 📝 |
| **États** | Impression et rapports | 📄 |
| **Macros** | Automatisation simple | ⚙️ |
| **Modules** | Code VBA | 💻 |

### 3.2 Création d'une Nouvelle Base de Données

#### Étapes de Création

1. **Lancer MS Access**
2. **Choisir "Base de données vide"**
3. **Nommer et enregistrer** le fichier (.accdb)
4. **Commencer la conception**

#### Démonstration Pratique

**Exercice guidé** : Créer une base de données "GestionEtudiants.accdb"

```
1. Ouvrir MS Access
2. Cliquer sur "Base de données vide"
3. Nom du fichier : GestionEtudiants
4. Cliquer sur "Créer"
```

### 3.3 Navigation et Composants

#### Le Volet de Navigation

- **Affichage par catégorie** : Tables, Requêtes, Formulaires...
- **Affichage par date** : Date de création ou modification
- **Recherche** : Barre de recherche d'objets

#### Les Vues de Travail

| Vue | Utilisation |
|-----|-------------|
| Mode Création | Conception de la structure |
| Mode Feuille de données | Saisie et visualisation |
| Mode Formulaire | Interface utilisateur |
| Mode SQL | Écriture de requêtes SQL |

### 3.4 Structuration et Organisation

#### Conventions de Nommage

**Préfixes recommandés** :

| Objet | Préfixe | Exemple |
|-------|---------|---------|
| Table | tbl | tblClient |
| Requête | qry | qryClientsActifs |
| Formulaire | frm | frmSaisieClient |
| État | rpt | rptListeClients |
| Macro | mcr | mcrOuvrirFormulaire |
| Module | mod | modFonctions |

#### Bonnes Pratiques de Nommage

- ✅ Noms explicites : `tblCommande` plutôt que `T1`
- ✅ Pas d'espaces : `tblLigneCommande` plutôt que `tbl Ligne Commande`
- ✅ Pas de caractères spéciaux : éviter accents, symboles
- ✅ Cohérence : utiliser les mêmes conventions partout

### 3.5 Sauvegarde et Restauration

#### Sauvegarde

**Méthodes de sauvegarde** :
1. **Copie du fichier .accdb** : La plus simple
2. **Compactage et réparation** : Optimise la base
3. **Export** : Vers d'autres formats

#### Compactage et Réparation

```
Outils de base de données → Compacter et réparer la base de données
```

**Avantages** :
- Réduit la taille du fichier
- Optimise les performances
- Répare les erreurs mineures

#### Bonnes Pratiques

- 📅 Sauvegarder régulièrement
- 📁 Conserver plusieurs versions
- 💾 Utiliser le cloud ou un support externe
- 🔄 Compacter avant sauvegarde

### Activité 4.2 : Création d'une Base de Données
**Durée : 15 minutes**

1. Créer une nouvelle base de données nommée "GestionCommerciale.accdb"
2. Explorer l'interface
3. Identifier les différents composants
4. Effectuer un compactage de la base

---

## Module 4 : MS Access - Tables Partie 1 (1h15)

### 4.1 Création de Tables en Mode Création

#### Accès au Mode Création

```
Onglet Créer → Table → Affichage → Mode Création
```

#### Interface du Mode Création

```
┌─────────────────────────────────────────────────────────────────┐
│ Nom du champ     │ Type de données    │ Description            │
├──────────────────┼────────────────────┼────────────────────────┤
│ NumClient        │ NuméroAuto         │ Identifiant unique     │
│ NomClient        │ Texte court        │ Nom du client          │
│ Email            │ Texte court        │ Adresse email          │
│ DateInscription  │ Date/Heure         │ Date d'inscription     │
├──────────────────┴────────────────────┴────────────────────────┤
│                    PROPRIÉTÉS DU CHAMP                         │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ Taille du champ    : 50                                    │ │
│ │ Format             :                                        │ │
│ │ Masque de saisie   :                                        │ │
│ │ Légende            : Nom du client                          │ │
│ │ Valeur par défaut  :                                        │ │
│ │ Valide si          :                                        │ │
│ │ Message si erreur  :                                        │ │
│ │ Null interdit      : Oui                                    │ │
│ │ Chaîne vide autorisée : Non                                 │ │
│ │ Indexé             : Non                                    │ │
│ └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

### 4.2 Types de Données dans Access

#### Types Disponibles

| Type | Description | Taille | Utilisation |
|------|-------------|--------|-------------|
| Texte court | Caractères | 0-255 | Noms, codes |
| Texte long | Caractères | Illimité | Descriptions |
| Numéro | Nombres | Variable | Quantités |
| NuméroAuto | Auto-incrément | 4 octets | Clés primaires |
| Monétaire | Montants | 8 octets | Prix, sommes |
| Date/Heure | Dates et heures | 8 octets | Dates |
| Oui/Non | Booléen | 1 bit | Cases à cocher |
| Objet OLE | Fichiers | Variable | Images, docs |
| Lien hypertexte | URLs | Variable | Liens web |
| Pièce jointe | Fichiers | Variable | Documents |
| Calculé | Formules | Variable | Champs dérivés |
| Assistant Liste | Liste de valeurs | Variable | Listes déroulantes |

### 4.3 Propriétés des Champs

#### Propriétés Générales

| Propriété | Description | Exemple |
|-----------|-------------|---------|
| Taille du champ | Longueur maximale | 50 caractères |
| Format | Affichage | Date courte |
| Masque de saisie | Format de saisie | 00000 (code postal) |
| Légende | Texte affiché | "Nom du client" |
| Valeur par défaut | Valeur initiale | Date() |
| Valide si | Règle de validation | >0 |
| Message si erreur | Message d'erreur | "Valeur positive requise" |
| Null interdit | Champ obligatoire | Oui/Non |
| Indexé | Création d'index | Oui - Sans doublons |

#### Exemples de Propriétés

**Champ Email** :
```
Taille du champ : 100
Valide si : Like "*@*.*"
Message si erreur : "Format email invalide"
Indexé : Oui - Sans doublons
```

**Champ Prix** :
```
Format : Monétaire
Valide si : >0
Message si erreur : "Le prix doit être positif"
Valeur par défaut : 0
```

### 4.4 Clés Primaires

#### Définition d'une Clé Primaire

1. Sélectionner le champ
2. Clic droit → "Clé primaire" ou bouton 🔑

#### Types de Clés Primaires

**Clé simple** :
- Un seul champ
- Ex: NumClient (NuméroAuto)

**Clé composée** :
- Plusieurs champs
- Sélectionner tous les champs (Ctrl+Clic)
- Définir comme clé primaire

#### Démonstration : Création de la Table CLIENT

```
Champs :
- NumClient    : NuméroAuto  → Clé primaire
- NomClient    : Texte(100)  → Null interdit
- PrenomClient : Texte(50)
- Email        : Texte(100)  → Indexé unique
- Telephone    : Texte(15)
- Adresse      : Texte(200)
- Ville        : Texte(50)
- CodePostal   : Texte(5)    → Masque: 00000
- DateInscr    : Date/Heure  → Défaut: Date()
```

### Activité 4.3 : Création de Tables
**Durée : 30 minutes**

Créez les tables suivantes dans votre base "GestionCommerciale" :

**Table tblProduit** :
| Champ | Type | Propriétés |
|-------|------|------------|
| RefProduit | Texte(10) | Clé primaire |
| Designation | Texte(100) | Obligatoire |
| PrixUnitaire | Monétaire | > 0 |
| QuantiteStock | Entier | >= 0, défaut 0 |
| SeuilAlerte | Entier | >= 0, défaut 10 |

**Table tblCategorie** :
| Champ | Type | Propriétés |
|-------|------|------------|
| CodeCategorie | Texte(5) | Clé primaire |
| LibelleCategorie | Texte(50) | Obligatoire |

---

## Module 5 : MS Access - Tables Partie 2 (1h30)

### 5.1 Saisie et Modification de Données

#### Mode Feuille de Données

```
Affichage → Mode Feuille de données
```

#### Opérations de Base

| Action | Méthode |
|--------|---------|
| Ajouter | Aller à la dernière ligne (*) |
| Modifier | Cliquer sur la cellule, modifier |
| Supprimer | Sélectionner la ligne, Suppr ou clic droit |
| Rechercher | Ctrl+F |
| Remplacer | Ctrl+H |

#### Navigation au Clavier

| Touche | Action |
|--------|--------|
| Tab | Champ suivant |
| Entrée | Enregistrer et ligne suivante |
| Échap | Annuler modification |
| Ctrl+; | Date du jour |
| Ctrl+: | Heure actuelle |

### 5.2 Validation et Masques de Saisie

#### Règles de Validation

**Opérateurs disponibles** :
- `>`, `<`, `>=`, `<=`, `<>` : Comparaisons
- `Between...And...` : Intervalle
- `Like` : Correspondance de motifs
- `In(...)` : Liste de valeurs
- `Is Null`, `Is Not Null` : Valeurs nulles

**Exemples** :

```
Prix > 0
Date >= #01/01/2020#
Statut In ("En cours", "Livré", "Annulé")
Email Like "*@*.*"
Age Between 18 And 65
```

#### Masques de Saisie

**Symboles** :
| Symbole | Signification |
|---------|---------------|
| 0 | Chiffre obligatoire (0-9) |
| 9 | Chiffre facultatif |
| # | Chiffre, espace, +, - |
| L | Lettre obligatoire (A-Z) |
| ? | Lettre facultative |
| A | Lettre ou chiffre obligatoire |
| a | Lettre ou chiffre facultatif |
| & | Tout caractère obligatoire |
| C | Tout caractère facultatif |
| < | Conversion en minuscules |
| > | Conversion en majuscules |

**Exemples pratiques** :

```
Code postal : 00000
Téléphone : 00\ 00\ 00\ 00\ 00
SIRET : 000\ 000\ 000\ 00000
Date : 00/00/0000
```

### 5.3 Formats d'Affichage

#### Formats Prédéfinis

**Dates** :
| Format | Exemple |
|--------|---------|
| Date, complet | mardi 15 janvier 2024 |
| Date, réduit | 15-jan-24 |
| Date, abrégé | 15/01/2024 |

**Nombres** :
| Format | Exemple |
|--------|---------|
| Nombre général | 1234,5678 |
| Monétaire | 1 234,57 € |
| Pourcentage | 123 456,78% |
| Scientifique | 1,23E+03 |

#### Formats Personnalisés

**Syntaxe** : `Format positif; Format négatif; Format zéro; Format null`

**Exemples** :
```
Monétaire : #,##0.00" €";-#,##0.00" €";"0,00 €"
Pourcentage : 0.00%
Texte majuscules : >
```

### 5.4 Import/Export de Données

#### Import depuis Excel

1. **Données externes** → **Nouvelle source de données** → **À partir d'un fichier** → **Excel**
2. Sélectionner le fichier
3. Choisir la feuille
4. Options d'importation :
   - Importer dans une nouvelle table
   - Ajouter à une table existante
5. Définir les types de données
6. Définir la clé primaire
7. Nommer la table

#### Import depuis CSV

1. **Données externes** → **Fichier texte**
2. Sélectionner le fichier
3. Choisir le délimiteur (virgule, point-virgule, tabulation)
4. Définir les types de données
5. Importer

#### Export vers Excel

1. Sélectionner la table
2. **Données externes** → **Excel**
3. Choisir le nom et l'emplacement
4. Options d'exportation

#### Export vers CSV

1. Sélectionner la table
2. **Données externes** → **Fichier texte**
3. Choisir le format (délimité)
4. Sélectionner le délimiteur

### Activité 4.4 : Manipulation de Données
**Durée : 30 minutes**

1. **Saisie de données** :
   - Ajoutez 5 produits dans tblProduit
   - Ajoutez 3 catégories dans tblCategorie

2. **Validation** :
   - Configurez une validation sur PrixUnitaire (> 0)
   - Ajoutez un masque de saisie pour RefProduit (format: AAA-0000)

3. **Import** :
   - Importez le fichier Excel fourni "produits_import.xlsx"
   - Vérifiez les données importées

---

## Synthèse de la Journée

### Points Clés à Retenir

1. **MPD** = implémentation technique du MLD (types, contraintes, index)
2. **MS Access** offre une interface visuelle pour créer des bases de données
3. **Mode Création** permet de définir la structure des tables
4. **Propriétés des champs** assurent l'intégrité des données
5. **Import/Export** facilite l'échange avec Excel et CSV

### Vocabulaire Technique

| Terme | Définition |
|-------|------------|
| MPD | Modèle Physique de Données |
| NuméroAuto | Type générant des identifiants uniques |
| Masque de saisie | Modèle de format pour la saisie |
| Validation | Règle vérifiant la cohérence des données |
| Index | Structure accélérant les recherches |

### Préparation pour le Jour 5

**À pratiquer** :
- Création de tables en mode création
- Configuration des propriétés des champs
- Saisie et modification de données

**À préparer** :
- Base de données avec les tables créées aujourd'hui
- Données de test saisies

---

## Ressources Complémentaires

- [Exercices supplémentaires - Jour 4](./activites/exercices_jour4.md)
- [Corrigés des exercices](./corriges/corriges_jour4.md)
- [Fichier exemple : produits_import.xlsx](./ressources/)
