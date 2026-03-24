# Corrigés Jour 3 - MCD et MLD

## Exercice 1 : Transformation MCD → MLD - Cas Simples

### Cas 1 : Relation 1:N Simple

**MLD** :
```
CLASSE (CodeClasse, Libelle, Niveau)
        └─ PK ────┘

ETUDIANT (NumEtud, Nom, Prenom, #CodeClasse)
          └─ PK ─┘              └─── FK ───┘
```

**Explication** : La clé primaire du côté "1" (CLASSE) migre comme clé étrangère vers le côté "N" (ETUDIANT).

### Cas 2 : Relation N:M Simple

**MLD** :
```
AUTEUR (CodeAuteur, NomAuteur)
        └─ PK ────┘

LIVRE (ISBN, Titre)
       └ PK ┘

ECRIT (#CodeAuteur, #ISBN)
       └────── PK ─────┘
```

**Explication** : La relation N:M génère une table associative avec les deux clés primaires.

### Cas 3 : Relation N:M avec Attributs

**MLD** :
```
EMPLOYE (Matricule, NomEmploye)
         └─ PK ──┘

PROJET (CodeProjet, Intitule)
        └─ PK ────┘

PARTICIPATION (#Matricule, #CodeProjet, NbHeures, Role)
               └───────── PK ─────────┘
```

**Explication** : Les attributs de la relation (NbHeures, Role) sont ajoutés à la table associative.

### Cas 4 : Relation 1:1

**MLD (Option 1 - FK dans la table optionnelle)** :
```
PERSONNE (NumPersonne, Nom, Prenom)
          └─ PK ─────┘

PERMIS_CONDUITE (NumPermis, DateObtention, Categories, #NumPersonne)
                 └─ PK ───┘                            └─── FK ───┘
```

**Explication** : Dans une relation 1:1, la FK va généralement du côté optionnel (0,1) vers le côté obligatoire (1,1).

---

## Exercice 2 : Transformation MCD → MLD - Cas Complexes

### Cas 1 : Relation Ternaire

**MLD** :
```
PROFESSEUR (NumProf, NomProf)
            └ PK ─┘

MATIERE (CodeMatiere, LibMatiere)
         └─ PK ────┘

CLASSE (CodeClasse, NomClasse)
        └─ PK ────┘

ENSEIGNE (#NumProf, #CodeMatiere, #CodeClasse, NbHeures)
          └────────────── PK ──────────────┘
```

**Clé primaire** : Composée des trois clés étrangères (NumProf, CodeMatiere, CodeClasse)

### Cas 2 : Association Réflexive

**MLD** :
```
EMPLOYE (Matricule, NomEmploye, Prenom, Poste, #MatriculeResponsable)
         └─ PK ──┘                            └──────── FK ─────────┘
```

**Explication** : L'entité contient une clé étrangère référençant sa propre clé primaire. Cette FK peut être NULL pour les employés au sommet de la hiérarchie.

### Cas 3 : Double Relation entre Entités

**MLD** :
```
ADRESSE (CodeAdresse, Rue, Ville, CodePostal)
         └─ PK ─────┘

CLIENT (NumClient, NomClient, #CodeAdresseLivraison, #CodeAdresseFacturation)
        └─ PK ───┘            └────── FK ─────────┘  └────── FK ──────────┘
```

**Explication** : Chaque relation génère sa propre clé étrangère, avec des noms distincts pour les différencier.

---

## Exercice 3 : Transformation Complète

**MLD Final** :

```
CATEGORIE (CodeCategorie, LibCategorie)
           └─ PK ───────┘

CLIENT (NumClient, NomClient, Adresse, Email, Telephone)
        └─ PK ───┘

PRODUIT (RefProduit, Designation, PrixUnitaire, Stock, #CodeCategorie)
         └─ PK ────┘                                   └──── FK ─────┘

COMMANDE (NumCommande, DateCommande, Statut, MontantTotal, #NumClient)
          └─ PK ─────┘                                     └── FK ───┘

LIGNE_COMMANDE (#NumCommande, #RefProduit, Quantite)
                └──────────── PK ────────┘
```

**Résumé des transformations** :
1. CATEGORIE → PRODUIT : Relation 1:N, FK dans PRODUIT
2. CLIENT → COMMANDE : Relation 1:N, FK dans COMMANDE
3. COMMANDE → PRODUIT (contient) : Relation N:M, table LIGNE_COMMANDE

---

## Exercice 4 : Vérification de Cohérence

### Erreurs identifiées

1. **Redondance NomClient et Adresse dans COMMANDE**
   - Ces informations sont déjà dans CLIENT
   - Solution : Utiliser une FK vers CLIENT

2. **Clé étrangère NumClient manquante dans COMMANDE**
   - Pas de lien vers CLIENT
   - Solution : Ajouter #NumClient

3. **Redondance PrixUnitaire et Designation dans LIGNE_COMMANDE**
   - Ces informations sont dans PRODUIT
   - Solution : Les retirer (sauf si historique nécessaire)

4. **Clé primaire incomplète dans LIGNE_COMMANDE**
   - Manque NumCommande
   - Solution : PK = (NumCommande, RefProduit)

### MLD Corrigé

```
CLIENT (NumClient, NomClient, Adresse)
        └─ PK ───┘

COMMANDE (NumCommande, DateCommande, #NumClient)
          └─ PK ─────┘              └── FK ───┘

PRODUIT (RefProduit, Designation, PrixUnitaire)
         └─ PK ────┘

LIGNE_COMMANDE (#NumCommande, #RefProduit, Quantite)
                └──────────── PK ────────┘
```

---

## Exercice 5 : Dictionnaire de Données

| Table | Champ | Type | Taille | Clé | Obligatoire | Description |
|-------|-------|------|--------|-----|-------------|-------------|
| EMPLOYE | Matricule | Texte | 10 | PK | Oui | Identifiant employé |
| EMPLOYE | Nom | Texte | 50 | - | Oui | Nom de famille |
| EMPLOYE | Prenom | Texte | 50 | - | Oui | Prénom |
| EMPLOYE | DateEmbauche | Date | - | - | Oui | Date d'entrée |
| EMPLOYE | Salaire | Monétaire | - | - | Oui | Salaire mensuel |
| EMPLOYE | CodeService | Texte | 5 | FK | Oui | Réf. service |
| SERVICE | CodeService | Texte | 5 | PK | Oui | Identifiant service |
| SERVICE | NomService | Texte | 50 | - | Oui | Nom du service |
| SERVICE | Localisation | Texte | 50 | - | Non | Lieu |
| PROJET | CodeProjet | Texte | 10 | PK | Oui | Identifiant projet |
| PROJET | Intitule | Texte | 100 | - | Oui | Nom du projet |
| PROJET | DateDebut | Date | - | - | Oui | Date de début |
| PROJET | DateFin | Date | - | - | Non | Date de fin |
| PROJET | Budget | Monétaire | - | - | Non | Budget alloué |
| PARTICIPATION | Matricule | Texte | 10 | PK, FK | Oui | Réf. employé |
| PARTICIPATION | CodeProjet | Texte | 10 | PK, FK | Oui | Réf. projet |
| PARTICIPATION | NbHeures | Entier | - | - | Oui | Heures travaillées |
| PARTICIPATION | Role | Texte | 30 | - | Non | Rôle dans le projet |

---

## Exercice 6 : Analyse et Critique de MLD

### Analyse

**1. Ce MLD n'est pas en 3FN** :

- Dans ETUDIANT : NomClasse dépend de CodeClasse (redondance)
- Dans CLASSE : NomProf dépend de NumProfPrincipal (redondance)
- Dans PROFESSEUR : LibMatiere dépend de CodeMatiere (redondance)

**2. Redondances identifiées** :

| Table | Champ redondant | Devrait être dans |
|-------|-----------------|-------------------|
| ETUDIANT | NomClasse | CLASSE |
| CLASSE | NomProf | PROFESSEUR |
| PROFESSEUR | LibMatiere | MATIERE |

### MLD Optimisé

```
MATIERE (CodeMatiere, LibMatiere, Coefficient)
         └─ PK ─────┘

PROFESSEUR (NumProf, NomProf, PrenomProf, Email, #CodeMatiere)
            └ PK ─┘                              └─── FK ───┘

CLASSE (CodeClasse, NomClasse, Niveau, Annee, #NumProfPrincipal)
        └─ PK ────┘                            └──── FK ──────┘

ETUDIANT (NumEtudiant, NomEtudiant, PrenomEtudiant, DateNaissance,
          └─ PK ─────┘
          AdresseRue, AdresseVille, AdresseCP, Email, Telephone, #CodeClasse)
                                                                  └── FK ───┘

NOTE (#NumEtudiant, #CodeMatiere, Valeur, DateEvaluation, TypeEval)
      └─────────── PK ─────────┘
```

---

## Exercice 7 : Gestion Hospitalière

### MCD Complété

```
┌─────────────────┐        ┌─────────────────┐        ┌─────────────────┐
│     PATIENT     │        │     SEJOUR      │        │    CHAMBRE      │
├─────────────────┤  1,n   ├─────────────────┤   0,n  ├─────────────────┤
│ NumPatient (PK) │────────│ NumSejour (PK)  │────────│ NumChambre (PK) │
│ NomPatient      │ a      │ DateEntree      │occupe  │ TypeChambre     │
│ DateNaissance   │        │ DateSortie      │        │ Etage           │
│ NumSecu         │        │ Motif           │        └─────────────────┘
└─────────────────┘        └────────┬────────┘
                                    │
                               0,n  │ fait_objet
                                    │ DateActe
                                    │
                           ┌────────┴────────┐        ┌─────────────────┐
                           │      ACTE       │   1,n  │    MEDECIN      │
                           ├─────────────────┤────────├─────────────────┤
                           │ CodeActe (PK)   │realise │ NumMedecin (PK) │
                           │ LibActe         │   0,n  │ NomMedecin      │
                           │ Tarif           │        │ Specialite      │
                           └─────────────────┘        └─────────────────┘
```

### MLD

```
PATIENT (NumPatient, NomPatient, DateNaissance, NumSecu)
         └─ PK ────┘

MEDECIN (NumMedecin, NomMedecin, Specialite)
         └─ PK ────┘

CHAMBRE (NumChambre, TypeChambre, Etage)
         └─ PK ────┘

ACTE (CodeActe, LibActe, Tarif)
      └ PK ──┘

SEJOUR (NumSejour, DateEntree, DateSortie, Motif, #NumPatient, #NumChambre)
        └─ PK ──┘                                 └─ FK ─────┘ └── FK ───┘

ACTE_REALISE (#NumSejour, #CodeActe, #NumMedecin, DateActe)
              └──────────── PK ───────────────┘
```

---

## Exercice 8 : Optimisation

### 1. Données calculées ou dérivées

| Table | Champ | Type | Justification |
|-------|-------|------|---------------|
| CLIENT | NbCommandes | Calculé | COUNT des commandes |
| CLIENT | MontantTotalAchats | Calculé | SUM des montants |
| COMMANDE | MontantTTC | Calculé | MontantHT + MontantTVA |
| PRODUIT | NbVentes | Calculé | SUM des quantités |
| LIGNE_COMMANDE | MontantLigne | Calculé | Quantite * PrixUnitaire |

### 2. Redondances acceptables pour performance

- **DesignationProduit dans LIGNE_COMMANDE** : Acceptable si historique nécessaire (le produit peut changer de nom)
- **NomCategorie dans PRODUIT** : Évite une jointure fréquente
- **PrixUnitaire dans LIGNE_COMMANDE** : Nécessaire pour garder le prix au moment de la commande

### 3. Index recommandés

```
-- Clés étrangères (jointures fréquentes)
CREATE INDEX idx_commande_client ON COMMANDE(IdClient);
CREATE INDEX idx_ligne_commande ON LIGNE_COMMANDE(IdCommande);
CREATE INDEX idx_ligne_produit ON LIGNE_COMMANDE(IdProduit);
CREATE INDEX idx_produit_categorie ON PRODUIT(IdCategorie);

-- Colonnes de recherche
CREATE INDEX idx_client_email ON CLIENT(Email);
CREATE INDEX idx_commande_date ON COMMANDE(DateCommande);
CREATE INDEX idx_commande_statut ON COMMANDE(Statut);
CREATE INDEX idx_produit_designation ON PRODUIT(Designation);
```

---

## Exercice 9 : Questions Théoriques

### Question 1 : Relation 1:N sans table supplémentaire
La clé primaire du côté "1" peut simplement être ajoutée comme clé étrangère dans la table du côté "N". Cela représente correctement la relation sans créer de table intermédiaire.

### Question 2 : Fusion d'entités 1:1
- Quand les deux entités ont les mêmes règles de gestion
- Quand l'une est toujours présente avec l'autre (1,1 des deux côtés)
- Quand cela simplifie les requêtes sans perte d'information

### Question 3 : Entité faible en MLD
- Son identifiant inclut la clé étrangère de l'entité forte
- La clé primaire est composée : FK + identifiant local
- Exemple : LIGNE_COMMANDE avec PK = (NumCommande, NumLigne)

### Question 4 : Clé naturelle vs artificielle

**Clé naturelle** :
- Exemples : ISBN, NumSecu, SIRET, Email
- Avantages : Signification métier
- Inconvénients : Peut changer, longueur variable

**Clé artificielle** :
- Exemples : ID auto-incrémenté
- Avantages : Stable, performante
- Inconvénients : Pas de sens métier

### Question 5 : FK nullable et intégrité
- Permet des relations optionnelles
- Risque : Orphelins possibles si mal gérés
- Solution : Contraintes CHECK ou triggers

---

## Exercice Bonus : Rétro-Ingénierie

### MCD Reconstitué

```
┌───────────────┐  1,n           0,n  ┌───────────────┐
│    AUTEUR     │─────────────────────│    LIVRE      │
├───────────────┤    ecrit           ├───────────────┤
│ IdAuteur (PK) │    RoleAuteur      │ ISBN (PK)     │
│ NomAuteur     │                    │ Titre         │
│ PaysOrigine   │                    │ AnneePublication
└───────────────┘                    │ Prix          │
                                     └───────┬───────┘
                                             │ 0,n
                                        ┌────┴────┐
                                        │ publie  │
                                        └────┬────┘
                                             │ 1,n
                                     ┌───────┴───────┐
                                     │   EDITEUR     │
                                     ├───────────────┤
                                     │ IdEditeur(PK) │
                                     │ NomEditeur    │
                                     │ Ville         │
                                     └───────────────┘

┌───────────────┐  1,n           0,n  ┌───────────────┐
│ BIBLIOTHEQUE  │─────────────────────│  EXEMPLAIRE   │
├───────────────┤    possede         ├───────────────┤
│IdBibliotheque │                    │IdExemplaire   │
│ NomBib        │                    │DateAcquisition│
│ Adresse       │                    │ Etat          │
└───────┬───────┘                    └───────┬───────┘
        │                                    │ 0,n
        │ 0,n                           ┌────┴────┐
   ┌────┴────┐                          │emprunte │
   │ inscrit │                          │DateEmprunt
   └────┬────┘                          │DateRetourP
        │ 1,n                           │DateRetourE
┌───────┴───────┐                       └────┬────┘
│   ADHERENT    │                            │ 0,n
├───────────────┤                            │
│ IdAdherent    │────────────────────────────┘
│ Nom           │
│ Prenom        │
│ DateAdhesion  │
└───────────────┘
```
