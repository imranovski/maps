# Corrigés Jour 4 - MPD et MS Access

## Exercice 1 : Définition des Types de Données

| Attribut | Type Access | Taille/Format | Justification |
|----------|-------------|---------------|---------------|
| NuméroClient | NuméroAuto | - | Clé primaire auto-incrémentée |
| NomClient | Texte court | 100 | Chaîne de caractères limitée |
| DateNaissance | Date/Heure | Date courte | Stockage de date |
| Email | Texte court | 100 | Format texte avec validation |
| Salaire | Monétaire | - | Montant avec 4 décimales |
| QuantitéStock | Numéro (Entier) | - | Nombres entiers positifs |
| Actif (oui/non) | Oui/Non | - | Valeur booléenne |
| Photo | Pièce jointe | - | Stockage de fichiers image |
| Description longue | Texte long | - | Texte sans limite |
| CodePostal | Texte court | 5 | Conservation des zéros initiaux |
| Téléphone | Texte court | 14 | Format avec espaces |
| SiteWeb | Lien hypertexte | - | URL cliquable |
| NuméroSécuritéSociale | Texte court | 15 | Format fixe avec chiffres |
| PrixUnitaire | Monétaire | - | Montant monétaire |

---

## Exercice 2 : Création du MPD

### Table ETUDIANT

| Champ | Type | Taille | PK/FK | Obligatoire | Défaut | Validation | Message |
|-------|------|--------|-------|-------------|--------|------------|---------|
| NumEtud | NuméroAuto | - | PK | Oui | Auto | - | - |
| Nom | Texte | 50 | - | Oui | - | - | Le nom est obligatoire |
| Prenom | Texte | 50 | - | Oui | - | - | Le prénom est obligatoire |
| DateNaissance | Date/Heure | - | - | Oui | - | <Date() | Date invalide |
| Email | Texte | 100 | - | Non | - | Like "*@*.*" | Format email invalide |
| Telephone | Texte | 14 | - | Non | - | - | - |
| CodeClasse | Texte | 10 | FK | Oui | - | - | - |

### Table CLASSE

| Champ | Type | Taille | PK/FK | Obligatoire | Défaut | Validation | Message |
|-------|------|--------|-------|-------------|--------|------------|---------|
| CodeClasse | Texte | 10 | PK | Oui | - | - | - |
| NomClasse | Texte | 50 | - | Oui | - | - | - |
| Niveau | Texte | 20 | - | Oui | - | In("1ère","2ème","3ème") | Niveau invalide |
| Annee | Texte | 9 | - | Oui | - | Like "####-####" | Format: 2024-2025 |

### Table MATIERE

| Champ | Type | Taille | PK/FK | Obligatoire | Défaut | Validation | Message |
|-------|------|--------|-------|-------------|--------|------------|---------|
| CodeMatiere | Texte | 10 | PK | Oui | - | - | - |
| Libelle | Texte | 50 | - | Oui | - | - | - |
| Coefficient | Numéro | Réel simple | - | Oui | 1 | Between 0.5 And 5 | Coefficient entre 0.5 et 5 |

### Table NOTE

| Champ | Type | Taille | PK/FK | Obligatoire | Défaut | Validation | Message |
|-------|------|--------|-------|-------------|--------|------------|---------|
| NumEtud | Numéro | Entier long | PK, FK | Oui | - | - | - |
| CodeMatiere | Texte | 10 | PK, FK | Oui | - | - | - |
| Valeur | Numéro | Réel simple | - | Oui | - | Between 0 And 20 | Note entre 0 et 20 |
| DateEvaluation | Date/Heure | - | - | Oui | Date() | <=Date() | Date future non autorisée |
| Appreciation | Texte | 200 | - | Non | - | - | - |

---

## Exercice 3 : Masques de Saisie

| Champ | Masque de saisie | Exemple | Explication |
|-------|------------------|---------|-------------|
| Code Postal | 00000 | 75001 | 5 chiffres obligatoires |
| Téléphone | 00\ 00\ 00\ 00\ 00 | 01 23 45 67 89 | Espaces automatiques |
| SIRET | 000\ 000\ 000\ 00000 | 123 456 789 01234 | 14 chiffres formatés |
| ISBN | 000\-0\-00\-000000\-0 | 978-2-12-345678-9 | Format ISBN-13 |
| Immatriculation | >LL\-000\-LL | AB-123-CD | Majuscules auto |
| Date | 00/00/0000 | 15/01/2024 | Format français |

---

## Exercice 4 : Règles de Validation

| Contrainte | Règle de validation | Message d'erreur |
|------------|---------------------|------------------|
| Prix > 0 | >0 | Le prix doit être supérieur à 0 |
| Quantité 0-9999 | Between 0 And 9999 | La quantité doit être entre 0 et 9999 |
| Date non future | <=Date() | La date ne peut pas être dans le futur |
| Email avec @ | Like "*@*.*" | L'email doit contenir un @ et un domaine |
| Statut valide | In("En cours","Livré","Annulé") | Statut invalide |
| Date fin > Date début | >[DateDebut] | La date de fin doit être après la date de début |
| Code commence par lettre | Like "[A-Z]*" | Le code doit commencer par une lettre |
| Note 0-20 | Between 0 And 20 | La note doit être entre 0 et 20 |

---

## Exercice 5 : Création de Tables Access

### Table tblClient - Corrigé

```
Nom du champ     Type de données    Description
─────────────────────────────────────────────────
NumClient        NuméroAuto         Clé primaire
RaisonSociale    Texte court (100)  Nom de l'entreprise
Adresse          Texte court (200)  Adresse postale
CodePostal       Texte court (5)    Code postal
Ville            Texte court (50)   Ville
Telephone        Texte court (14)   Numéro de téléphone
Email            Texte court (100)  Adresse email
DateCreation     Date/Heure         Date de création
Actif            Oui/Non            Client actif

Propriétés importantes :
- NumClient : Clé primaire (automatique avec NuméroAuto)
- RaisonSociale : Null interdit = Oui
- CodePostal : Masque de saisie = 00000
- Telephone : Masque de saisie = 00\ 00\ 00\ 00\ 00
- Email : Valide si = Like "*@*.*"
         Message si erreur = "Format email invalide"
- DateCreation : Valeur par défaut = Date()
- Actif : Valeur par défaut = Oui
```

### Table tblProduit - Corrigé

```
Nom du champ     Type de données    Description
─────────────────────────────────────────────────
RefProduit       Texte court (10)   Référence produit
Designation      Texte court (100)  Nom du produit
Description      Texte long         Description détaillée
PrixAchat        Monétaire          Prix d'achat
PrixVente        Monétaire          Prix de vente
QuantiteStock    Numéro (Entier)    Stock actuel
SeuilAlerte      Numéro (Entier)    Seuil de réapprovisionnement
CodeCategorie    Texte court (5)    Catégorie du produit
DateCreation     Date/Heure         Date de création

Propriétés importantes :
- RefProduit : Clé primaire (manuelle)
              Format = >LL\-0000 (ex: AB-1234)
- Designation : Null interdit = Oui
- PrixAchat : Valide si = >=0
              Message si erreur = "Le prix d'achat doit être positif"
- PrixVente : Valide si = >[PrixAchat]
              Message si erreur = "Le prix de vente doit être supérieur au prix d'achat"
- QuantiteStock : Valeur par défaut = 0
                  Valide si = >=0
- SeuilAlerte : Valeur par défaut = 10
- DateCreation : Valeur par défaut = Date()
```

### Table tblCommande - Corrigé

```
Nom du champ     Type de données    Description
─────────────────────────────────────────────────
NumCommande      NuméroAuto         Numéro de commande
DateCommande     Date/Heure         Date de la commande
NumClient        Numéro (Entier long) Référence client
Statut           Texte court (20)   État de la commande
MontantHT        Monétaire          Montant hors taxes
TauxRemise       Numéro (Réel simple) Taux de remise
Commentaire      Texte long         Remarques

Propriétés importantes :
- NumCommande : Clé primaire
- DateCommande : Null interdit = Oui
                 Valeur par défaut = Date()
- NumClient : Null interdit = Oui (clé étrangère)
- Statut : Valide si = In("En cours","Expédié","Livré","Annulé")
           Valeur par défaut = "En cours"
- TauxRemise : Valide si = Between 0 And 0.5
               Message si erreur = "Le taux de remise doit être entre 0 et 50%"
```

---

## Exercice 6 : Import de Données

### Vérifications avant import

1. **Format des données** :
   - Vérifier que les colonnes correspondent aux champs Access
   - Vérifier les types (nombres, dates, texte)
   - Supprimer les lignes vides ou en-têtes multiples

2. **Cohérence** :
   - Pas de doublons sur les clés
   - Valeurs valides selon les contraintes

3. **Encodage** :
   - UTF-8 ou ANSI selon les accents

### Gestion des types

| Colonne Excel | Type suggéré par Access | Action recommandée |
|---------------|-------------------------|-------------------|
| Reference | Texte | Vérifier : conserver comme clé primaire |
| Nom_Produit | Texte | OK |
| Prix | Monétaire | Convertir en nombre avec 2 décimales |
| Stock | Entier | Vérifier : pas de valeurs négatives |
| Categorie | Texte | Vérifier cohérence avec table catégories |

### Gestion des erreurs

- Créer une table de rejet pour les lignes en erreur
- Examiner les valeurs nulles
- Corriger les formats de date (JJ/MM/AAAA vs MM/JJ/AAAA)

---

## Exercice 7 : Export de Données

### Export vers Excel

1. Sélectionner la table ou requête
2. Données externes → Excel
3. Choisir le format .xlsx
4. Options : ☑ Exporter avec mise en forme
5. Valider

### Export vers CSV

1. Sélectionner la table
2. Données externes → Fichier texte
3. Choisir "Délimité"
4. Sélectionner le séparateur (point-virgule pour Excel français)
5. Inclure les noms de champs en première ligne

### Export vers PDF

1. Créer un état basé sur la requête/table
2. Fichier → Exporter → PDF
3. Ou clic droit sur l'état → Exporter → PDF

---

## Exercice 8 : Cas Pratique Bibliothèque

### Table tblLivre

```sql
CREATE TABLE tblLivre (
    ISBN TEXT(13) PRIMARY KEY,
    Titre TEXT(200) NOT NULL,
    Auteur TEXT(100),
    Editeur TEXT(100),
    AnneePublication INTEGER CHECK (AnneePublication >= 1900 AND AnneePublication <= Year(Date())),
    NbExemplaires INTEGER DEFAULT 1 CHECK (NbExemplaires >= 1),
    Categorie TEXT(20) CHECK (Categorie IN ('Roman','BD','Manuel','Documentaire'))
);
```

### Table tblAdherent

```sql
CREATE TABLE tblAdherent (
    NumAdherent AUTOINCREMENT PRIMARY KEY,
    Nom TEXT(50) NOT NULL,
    Prenom TEXT(50) NOT NULL,
    DateNaissance DATE,
    Email TEXT(100) UNIQUE,
    Telephone TEXT(14),
    DateInscription DATE DEFAULT Date(),
    TypeAdherent TEXT(20) CHECK (TypeAdherent IN ('Étudiant','Enseignant','Externe'))
);
```

### Table tblEmprunt

```sql
CREATE TABLE tblEmprunt (
    NumEmprunt AUTOINCREMENT PRIMARY KEY,
    ISBN TEXT(13) REFERENCES tblLivre(ISBN),
    NumAdherent INTEGER REFERENCES tblAdherent(NumAdherent),
    DateEmprunt DATE DEFAULT Date(),
    DateRetourPrevue DATE,
    DateRetourEffective DATE,
    Statut TEXT(20) DEFAULT 'En cours' CHECK (Statut IN ('En cours','Retourné','En retard'))
);
```

---

## Exercice 9 : Questions de Réflexion

### Question 1 : Texte pour codes postaux
Les codes postaux peuvent commencer par 0 (ex: 06000 Nice). Un type numérique perdrait ce zéro initial. De plus, les codes postaux ne font pas l'objet de calculs mathématiques.

### Question 2 : NuméroAuto - Avantages/Inconvénients

**Avantages** :
- Unicité garantie
- Génération automatique
- Performances (indexation sur entiers)
- Stable (ne change jamais)

**Inconvénients** :
- Pas de signification métier
- Valeurs peuvent avoir des "trous" après suppressions
- Difficile à communiquer aux utilisateurs

### Question 3 : Champ multivalué
Créer une table séparée avec relation 1:N. Exemple :
```
EMPLOYE_COMPETENCE (#Matricule, Competence)
```

### Question 4 : Obligatoire vs Indexé
- **Obligatoire** : Garantit une valeur non nulle
- **Indexé** : Accélère les recherches et tris

Ce sont deux concepts indépendants.

### Question 5 : Champ Calculé vs Normal
Utiliser un champ calculé quand :
- La valeur dépend d'autres champs de la même table
- Pas besoin de stocker (gain de place)
- Toujours à jour automatiquement

Utiliser un champ normal quand :
- Valeur indépendante
- Performances critiques (évite le recalcul)
- Historique nécessaire

---

## Exercice 10 : Base de Données Magasin

### MCD

```
┌─────────────┐  1,n        0,n  ┌─────────────┐
│  CATEGORIE  │──────────────────│   ARTICLE   │
├─────────────┤    appartient    ├─────────────┤
│ CodeCat     │                  │ RefArticle  │
│ LibelleCat  │                  │ Designation │
└─────────────┘                  │ Taille      │
                                 │ Couleur     │
                                 │ PrixVente   │
                                 │ Stock       │
                                 └──────┬──────┘
                                        │
                                   0,n  │ contient
                                        │ Quantite
                                        │ PrixLigne
                                        │
┌─────────────┐  1,n        0,n  ┌──────┴──────┐
│   CLIENT    │──────────────────│    VENTE    │
├─────────────┤    effectue      ├─────────────┤
│ NumClient   │                  │ NumVente    │
│ Nom         │                  │ DateVente   │
│ Prenom      │                  │ MontantTotal│
│ Adresse     │                  └─────────────┘
│ Fidelite    │
└─────────────┘
```

### MLD

```
CATEGORIE (CodeCat, LibelleCat)
CLIENT (NumClient, Nom, Prenom, Adresse, Fidelite)
ARTICLE (RefArticle, Designation, Taille, Couleur, PrixVente, Stock, #CodeCat)
VENTE (NumVente, DateVente, MontantTotal, #NumClient)
LIGNE_VENTE (#NumVente, #RefArticle, Quantite, PrixLigne)
```
