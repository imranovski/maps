# Jour 3 - Approfondissement MCD et Modèle Logique de Données (MLD)

## Durée : 6 heures

---

## Planning de la Journée

### Matinée (9h00 - 12h00) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 9h00 - 9h15 | Révision Jour 2 | Rappel MCD, Questions/Réponses | 15min |
| 9h15 - 11h00 | MCD - Approfondissement | Cas complexes, Exercices corrigés | 1h45 |
| 11h00 - 11h15 | PAUSE CAFÉ | | 15min |
| 11h15 - 12h00 | Modèle MLD - Partie 1 | Passage MCD→MLD, Règles de transformation | 45min |

### Après-midi (13h30 - 16h30) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 13h30 - 15h15 | Modèle MLD - Partie 2 | Clés, Associations, Optimisation | 1h45 |
| 15h15 - 15h30 | PAUSE | | 15min |
| 15h30 - 16h30 | Modèle MLD - Partie 3 | Cas pratiques, Vérification | 1h |

---

## Module 1 : Révision Jour 2 (15 min)

### Quiz de Révision

1. Quelles sont les trois formes normales ?
2. Qu'est-ce qu'une dépendance fonctionnelle ?
3. Donnez un exemple de relation ternaire.
4. Qu'est-ce qu'une association réflexive ?

### Points de Clarification

Discussion sur les difficultés rencontrées lors des exercices du Jour 2.

---

## Module 2 : MCD - Approfondissement (1h45)

### 2.1 Cas d'Étude 1 : Gestion de Bibliothèque

#### Contexte

Une bibliothèque municipale souhaite informatiser sa gestion. Le système doit gérer :

- **Les ouvrages** : ISBN, titre, auteur, éditeur, année, genre, nombre d'exemplaires
- **Les adhérents** : Numéro, nom, prénom, adresse, téléphone, date d'inscription
- **Les emprunts** : Date d'emprunt, date de retour prévue, date de retour effective
- **Les réservations** : Date de réservation, statut
- **Les pénalités** : Montant, motif, statut de paiement

#### Règles de Gestion

1. Un adhérent peut emprunter au maximum 5 ouvrages simultanément
2. La durée d'emprunt standard est de 21 jours
3. Une pénalité de 0,50€ par jour de retard est appliquée
4. Un adhérent peut réserver un ouvrage déjà emprunté
5. Un auteur peut avoir écrit plusieurs ouvrages

#### Modélisation MCD

```
┌─────────────────┐                           ┌─────────────────┐
│     AUTEUR      │                           │     EDITEUR     │
├─────────────────┤                           ├─────────────────┤
│ CodeAuteur (PK) │                           │ CodeEditeur(PK) │
│ NomAuteur       │                           │ NomEditeur      │
│ PrenomAuteur    │                           │ AdresseEditeur  │
│ Nationalite     │                           └────────┬────────┘
└────────┬────────┘                                    │
         │ 1,n                                         │ 1,n
         │                                             │
    ┌────┴────┐                                   ┌────┴────┐
    │  ecrit  │                                   │ publie  │
    └────┬────┘                                   └────┬────┘
         │ 0,n                                         │ 0,n
         │                                             │
         └──────────────────┬──────────────────────────┘
                            │
                   ┌────────┴────────┐
                   │     OUVRAGE     │
                   ├─────────────────┤
                   │ ISBN (PK)       │
                   │ Titre           │
                   │ AnneeParution   │
                   │ Genre           │
                   │ NbExemplaires   │
                   └────────┬────────┘
                            │
              ┌─────────────┼─────────────┐
              │             │             │
         0,n  │        0,n  │        0,n  │
         ┌────┴────┐   ┌────┴────┐   ┌────┴────┐
         │emprunte │   │reserve  │   │         │
         │DateEmpr │   │DateRes  │   │         │
         │DateRetP │   │Statut   │   │         │
         │DateRetE │   └────┬────┘   │         │
         └────┬────┘        │        │         │
              │        0,n  │        │         │
              │             │        │         │
              └─────────────┼────────┘         │
                            │                  │
                   ┌────────┴────────┐         │
                   │    ADHERENT     │         │
                   ├─────────────────┤         │
                   │ NumAdherent(PK) │◄────────┘
                   │ Nom             │  0,n   1,n
                   │ Prenom          │  PENALITE
                   │ Adresse         │  Montant
                   │ Telephone       │  Motif
                   │ DateInscription │  Statut
                   └─────────────────┘
```

### 2.2 Cas d'Étude 2 : Système de Réservation

#### Contexte

Un système de réservation de salles de réunion dans une entreprise :

- **Les salles** : Numéro, capacité, équipements
- **Les employés** : Matricule, nom, département
- **Les réservations** : Date, heure début, heure fin, objet
- **Les équipements** : Type, quantité disponible

#### Règles de Gestion

1. Une salle peut avoir plusieurs équipements
2. Un employé peut faire plusieurs réservations
3. Une salle ne peut pas être réservée deux fois au même créneau
4. Certaines réservations peuvent nécessiter des équipements supplémentaires

#### Modélisation MCD

```
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│   DEPARTEMENT   │       │     EMPLOYE     │       │      SALLE      │
├─────────────────┤       ├─────────────────┤       ├─────────────────┤
│ CodeDept (PK)   │ 1,n   │ Matricule (PK)  │       │ NumSalle (PK)   │
│ NomDept         │◄──────│ NomEmploye      │       │ Capacite        │
│ Localisation    │  0,1  │ PrenomEmploye   │       │ Etage           │
└─────────────────┘       │ Poste           │       └────────┬────────┘
                          └────────┬────────┘                │
                                   │                         │
                              0,n  │                    0,n  │
                                   │                         │
                              ┌────┴────┐               ┌────┴────┐
                              │ reserve │               │ dispose │
                              │ Date    │               └────┬────┘
                              │HeureDebut                    │
                              │HeureFin │               0,n  │
                              │ Objet   │                    │
                              └────┬────┘          ┌─────────┴─────────┐
                                   │               │    EQUIPEMENT     │
                              0,n  │               ├───────────────────┤
                                   └───────────────│ CodeEquip (PK)    │
                                                   │ TypeEquip         │
                                                   │ QteDisponible     │
                                                   └───────────────────┘
```

### 2.3 Cas d'Étude 3 : Application Pédagogique Économie-Gestion

#### Contexte

Un professeur d'économie-gestion souhaite créer une base de données pédagogique pour simuler la gestion d'une entreprise commerciale avec ses élèves.

#### Entités à Modéliser

1. **Entreprises simulées** : SIRET, raison sociale, secteur d'activité
2. **Élèves** : Numéro, nom, classe, rôle dans l'entreprise simulée
3. **Transactions** : Achats, ventes entre entreprises
4. **Bilan simplifié** : Actif, passif, résultat

### Activité 3.1 : Modélisation Complète
**Durée : 30 minutes**

En groupe, modélisez le système pédagogique d'économie-gestion.

**Livrables** :
1. Liste des entités et attributs
2. MCD complet avec cardinalités
3. Justification des choix de modélisation

---

## Module 3 : Modèle MLD - Partie 1 (45 min)

### 3.1 Introduction au MLD

#### Définition

Le **Modèle Logique de Données (MLD)** est la traduction du MCD vers un modèle de données compatible avec un SGBD relationnel. Il décrit les tables, les colonnes et les relations.

#### Objectif

Transformer le MCD (indépendant de la technologie) en un schéma relationnel (orienté implémentation).

### 3.2 Règles de Transformation

#### Règle 1 : Transformation des Entités

**Principe** : Chaque entité devient une **table**. Chaque attribut devient une **colonne**. L'identifiant devient la **clé primaire**.

**MCD** :
```
┌─────────────────┐
│    ETUDIANT     │
├─────────────────┤
│ NumEtud (PK)    │
│ Nom             │
│ Prenom          │
│ DateNaissance   │
└─────────────────┘
```

**MLD** :
```
ETUDIANT (NumEtud, Nom, Prenom, DateNaissance)
         └─ PK ──┘
```

#### Règle 2 : Transformation des Relations 1:N

**Principe** : La clé primaire du côté "1" migre comme **clé étrangère** vers le côté "N".

**MCD** :
```
┌─────────────┐  1,1           1,n  ┌─────────────┐
│  ETUDIANT   │────────────────────│   CLASSE    │
├─────────────┤    appartient      ├─────────────┤
│ NumEtud(PK) │                    │ CodeClasse  │
│ Nom         │                    │ Libelle     │
└─────────────┘                    └─────────────┘
```

**MLD** :
```
CLASSE (CodeClasse, Libelle)
        └─ PK ──┘

ETUDIANT (NumEtud, Nom, #CodeClasse)
          └─ PK ──┘     └─── FK ───┘
```

*La clé étrangère est notée avec # ou en italique.*

#### Règle 3 : Transformation des Relations N:M

**Principe** : La relation devient une **table associative** contenant les clés primaires des deux entités comme clé primaire composée.

**MCD** :
```
┌─────────────┐  0,n           0,n  ┌─────────────┐
│  ETUDIANT   │────────────────────│    COURS    │
├─────────────┤    s'inscrit       ├─────────────┤
│ NumEtud(PK) │    DateInscription │ CodeCours   │
│ Nom         │    Note            │ Intitule    │
└─────────────┘                    └─────────────┘
```

**MLD** :
```
ETUDIANT (NumEtud, Nom)
          └─ PK ──┘

COURS (CodeCours, Intitule)
       └─ PK ──┘

INSCRIPTION (#NumEtud, #CodeCours, DateInscription, Note)
             └──────── PK ──────┘
```

#### Règle 4 : Transformation des Relations 1:1

**Principe** : La clé primaire d'une entité migre vers l'autre comme clé étrangère (généralement du côté optionnel).

**MCD** :
```
┌─────────────┐  1,1           0,1  ┌─────────────┐
│  PERSONNE   │────────────────────│  PASSEPORT  │
├─────────────┤    possède         ├─────────────┤
│ NumPers(PK) │                    │ NumPasseport│
│ Nom         │                    │ DateEmission│
└─────────────┘                    └─────────────┘
```

**MLD (Option 1)** :
```
PERSONNE (NumPers, Nom)
          └─ PK ──┘

PASSEPORT (NumPasseport, DateEmission, #NumPers)
           └─── PK ───┘                └─ FK ─┘
```

### 3.3 Exemples de Conversion

#### Exemple Complet : Gestion de Commandes

**MCD** :
```
┌─────────────┐  1,n           0,n  ┌─────────────┐
│   CLIENT    │────────────────────│   COMMANDE  │
├─────────────┤     passe          ├─────────────┤
│ NumClient   │                    │ NumCommande │
│ NomClient   │                    │ DateCommande│
└─────────────┘                    └──────┬──────┘
                                          │
                                     0,n  │
                                          │
                                     ┌────┴────┐
                                     │ contient│
                                     │ Quantite│
                                     └────┬────┘
                                          │
                                     0,n  │
                                          │
                                   ┌──────┴──────┐
                                   │   PRODUIT   │
                                   ├─────────────┤
                                   │ RefProduit  │
                                   │ Designation │
                                   │ PrixUnitaire│
                                   └─────────────┘
```

**MLD** :
```
CLIENT (NumClient, NomClient)
        └─ PK ──┘

COMMANDE (NumCommande, DateCommande, #NumClient)
          └─ PK ────┘               └─── FK ──┘

PRODUIT (RefProduit, Designation, PrixUnitaire)
         └─ PK ───┘

LIGNE_COMMANDE (#NumCommande, #RefProduit, Quantite)
                └──────────── PK ───────┘
```

### Activité 3.2 : Transformation MCD → MLD
**Durée : 20 minutes**

Transformez le MCD suivant en MLD :

```
┌─────────────┐  1,n           0,n  ┌─────────────┐
│ PROFESSEUR  │────────────────────│   MATIERE   │
├─────────────┤    enseigne        ├─────────────┤
│ NumProf     │    NbHeures        │ CodeMatiere │
│ NomProf     │                    │ LibMatiere  │
└─────────────┘                    └─────────────┘
```

---

## Module 4 : Modèle MLD - Partie 2 (1h45)

### 4.1 Gestion des Clés Primaires et Étrangères

#### Clé Primaire (PK)

**Caractéristiques** :
- Identifie de manière unique chaque enregistrement
- Ne peut pas être NULL
- Doit être stable (ne change pas dans le temps)

**Types de clés primaires** :
1. **Clé naturelle** : Attribut existant (ISBN, SIRET, Email)
2. **Clé artificielle** : Identifiant généré (auto-incrément)
3. **Clé composée** : Combinaison de plusieurs attributs

#### Clé Étrangère (FK)

**Caractéristiques** :
- Référence une clé primaire d'une autre table
- Peut être NULL (si relation optionnelle)
- Assure l'intégrité référentielle

**Notation dans le MLD** :
- Préfixe # : #NumClient
- Suffixe _FK : NumClient_FK
- Italique ou souligné pointillé

### 4.2 Transformation des Associations

#### Associations avec Attributs

Les attributs de l'association migrent vers :
- La table étrangère (1:N)
- La table associative (N:M)

**Exemple** :
```
MCD:
ETUDIANT ──(inscrit, Note, DateInscr)── COURS
   1,n                                    0,n

MLD:
INSCRIPTION (#NumEtud, #CodeCours, Note, DateInscr)
```

#### Associations Ternaires

Une association ternaire génère une table avec les trois clés étrangères.

**MCD** :
```
PROFESSEUR ─┐
            │
   ENSEIGNE ├─ NbHeures
            │
   MATIERE ─┤
            │
    CLASSE ─┘
```

**MLD** :
```
ENSEIGNE (#NumProf, #CodeMatiere, #CodeClasse, NbHeures)
          └────────────── PK ─────────────────┘
```

#### Associations Réflexives

L'entité contient une clé étrangère référençant sa propre clé primaire.

**MCD** :
```
EMPLOYE ──(dirige 0,1 - 0,n)── EMPLOYE
```

**MLD** :
```
EMPLOYE (NumEmp, NomEmp, #NumEmpResponsable)
         └─ PK ─┘        └────── FK ──────┘
```

### 4.3 Cas Particuliers

#### Relation 1:1 Obligatoire des Deux Côtés

**Options** :
1. Fusionner les deux entités
2. Choisir une entité pour recevoir la FK

#### Spécialisation/Généralisation

**Options** :

**Option 1 : Table unique avec type**
```
PERSONNE (NumPers, Type, Nom, Prenom, 
          NumEtud, Niveau, Filiere,  -- Attributs ETUDIANT (NULL si prof)
          NumProf, Grade, Specialite) -- Attributs PROFESSEUR (NULL si étudiant)
```

**Option 2 : Tables séparées avec FK**
```
PERSONNE (NumPers, Nom, Prenom)

ETUDIANT (NumEtud, Niveau, Filiere, #NumPers)

PROFESSEUR (NumProf, Grade, Specialite, #NumPers)
```

**Option 3 : Tables complètement séparées**
```
ETUDIANT (NumEtud, Nom, Prenom, Niveau, Filiere)

PROFESSEUR (NumProf, Nom, Prenom, Grade, Specialite)
```

### 4.4 Optimisation du Modèle Relationnel

#### Dénormalisation Contrôlée

Parfois, pour des raisons de performance, on accepte une légère redondance.

**Exemple** : Stocker le nom du client directement dans la commande pour éviter une jointure.

```
COMMANDE (NumCommande, DateCommande, #NumClient, NomClient)
```

⚠️ **Attention** : Risque d'incohérence si le nom change !

#### Index

Créer des index sur les colonnes fréquemment utilisées pour les recherches :
- Clés étrangères
- Colonnes de recherche courante

### Activité 3.3 : Optimisation
**Durée : 20 minutes**

Analysez le MLD suivant et proposez des améliorations :

```
COMMANDE (NumCommande, DateCommande, #NumClient)
LIGNE_COMMANDE (#NumCommande, #RefProduit, Quantite, PrixUnitaire, Designation)
CLIENT (NumClient, NomClient, AdresseClient)
PRODUIT (RefProduit, Designation, PrixUnitaire, Stock)
```

**Questions** :
1. Y a-t-il de la redondance ?
2. Quelles colonnes nécessitent un index ?
3. Proposez une version optimisée

---

## Module 5 : Modèle MLD - Partie 3 (1h)

### 5.1 Cas Pratique : Transformation Complète

#### Énoncé

Transformez le MCD de gestion de bibliothèque (vu ce matin) en MLD.

#### Solution Étape par Étape

**Étape 1 : Transformation des entités**
```
AUTEUR (CodeAuteur, NomAuteur, PrenomAuteur, Nationalite)
EDITEUR (CodeEditeur, NomEditeur, AdresseEditeur)
OUVRAGE (ISBN, Titre, AnneeParution, Genre, NbExemplaires)
ADHERENT (NumAdherent, Nom, Prenom, Adresse, Telephone, DateInscription)
```

**Étape 2 : Transformation de la relation N:M ECRIT**
```
ECRIT (#CodeAuteur, #ISBN)
```

**Étape 3 : Transformation de la relation 1:N PUBLIE**
```
OUVRAGE (ISBN, Titre, AnneeParution, Genre, NbExemplaires, #CodeEditeur)
```

**Étape 4 : Transformation de la relation N:M EMPRUNTE**
```
EMPRUNT (#NumAdherent, #ISBN, DateEmprunt, DateRetourPrevue, DateRetourEffective)
```

**Étape 5 : Transformation de la relation N:M RESERVE**
```
RESERVATION (#NumAdherent, #ISBN, DateReservation, Statut)
```

**Étape 6 : Transformation de la relation 1:N PENALITE**
```
PENALITE (NumPenalite, #NumAdherent, Montant, Motif, Statut)
```

#### MLD Final

```
AUTEUR (CodeAuteur, NomAuteur, PrenomAuteur, Nationalite)
        └─ PK ───┘

EDITEUR (CodeEditeur, NomEditeur, AdresseEditeur)
         └─ PK ────┘

OUVRAGE (ISBN, Titre, AnneeParution, Genre, NbExemplaires, #CodeEditeur)
         └ PK ┘                                             └─── FK ───┘

ECRIT (#CodeAuteur, #ISBN)
       └──── PK ────────┘

ADHERENT (NumAdherent, Nom, Prenom, Adresse, Telephone, DateInscription)
          └─ PK ────┘

EMPRUNT (#NumAdherent, #ISBN, DateEmprunt, DateRetourPrevue, DateRetourEffective)
         └──── PK ────────────────────┘

RESERVATION (#NumAdherent, #ISBN, DateReservation, Statut)
             └─────── PK ───────────────────────┘

PENALITE (NumPenalite, #NumAdherent, Montant, Motif, Statut)
          └─ PK ────┘  └─── FK ───┘
```

### 5.2 Vérification de la Cohérence

#### Checklist de Vérification

- [ ] Chaque table a une clé primaire
- [ ] Toutes les clés étrangères référencent une clé primaire existante
- [ ] Pas de redondance inutile
- [ ] Les types de données sont cohérents
- [ ] Les contraintes NOT NULL sont définies

#### Erreurs Courantes à Éviter

1. **Oubli d'une table associative** pour les relations N:M
2. **Mauvaise direction de la clé étrangère** dans les relations 1:N
3. **Clé primaire composée incomplète** dans les tables associatives
4. **Perte d'attributs** lors de la transformation

### 5.3 Exercice Guidé : Du MCD au MLD
**Durée : 30 minutes**

Transformez le MCD suivant :

```
┌─────────────┐          ┌─────────────┐          ┌─────────────┐
│   CLIENT    │          │   COMMANDE  │          │   ARTICLE   │
├─────────────┤   0,n    ├─────────────┤   0,n    ├─────────────┤
│ CodeClient  │◄─────────│ NumCommande │──────────│ RefArticle  │
│ NomClient   │   1,1    │ DateCommande│   contient│ LibArticle  │
│ Adresse     │  passe   │ Statut      │   Qte    │ PrixUnit    │
│ Email       │          └─────────────┘   1,n    │ Stock       │
└─────────────┘                                   └─────────────┘
```

**Travail demandé** :
1. Identifiez les tables
2. Définissez les clés primaires et étrangères
3. Écrivez le MLD complet

---

## Synthèse de la Journée

### Points Clés à Retenir

1. Le **MLD** est la traduction du MCD vers le modèle relationnel
2. **Règle entité → table** : Chaque entité devient une table
3. **Règle 1:N** : La clé primaire du côté "1" migre vers le côté "N"
4. **Règle N:M** : Création d'une table associative
5. La vérification de la cohérence est essentielle

### Tableau Récapitulatif des Transformations

| Élément MCD | Transformation MLD |
|-------------|-------------------|
| Entité | Table |
| Attribut | Colonne |
| Identifiant | Clé primaire |
| Relation 1:1 | FK dans une des tables |
| Relation 1:N | FK du côté N |
| Relation N:M | Table associative |
| Attribut de relation | Colonne de la FK ou table associative |

### Préparation pour le Jour 4

**À réviser** :
- Les règles de transformation MCD → MLD
- La gestion des clés primaires et étrangères
- Les cas particuliers de transformation

**Questions de réflexion** :
1. Comment présenter le passage MCD→MLD à vos élèves ?
2. Quels outils logiciels facilitent cette transformation ?

---

## Ressources Complémentaires

- [Exercices supplémentaires - Jour 3](./activites/exercices_jour3.md)
- [Corrigés des exercices](./corriges/corriges_jour3.md)
