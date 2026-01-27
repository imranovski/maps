# FICHE DE DÉROULEMENT - JOUR 3
## Approfondissement MCD et Modèle Logique de Données (MLD)

---

## 📋 INFORMATIONS DE LA SÉANCE

| Élément | Description |
|---------|-------------|
| **Jour** | Jour 3 sur 5 |
| **Durée** | 6 heures |
| **Thème** | Approfondissement MCD et MLD |
| **Public** | Professeurs d'Économie et Gestion |
| **Niveau** | Intermédiaire |

---

## 🎯 OBJECTIFS PÉDAGOGIQUES

À la fin de cette journée, les participants seront capables de :

1. Consolider les acquis sur le MCD avec des cas d'études complexes
2. Maîtriser les règles de passage du MCD au MLD
3. Transformer les différents types d'associations
4. Gérer les clés primaires et étrangères
5. Optimiser le modèle relationnel
6. Vérifier la cohérence d'un schéma relationnel

---

## 🛠️ MATÉRIEL ET RESSOURCES

### Matériel formateur
- [ ] Vidéoprojecteur
- [ ] Ordinateur avec présentation
- [ ] Tableau blanc et marqueurs
- [ ] Supports de cours imprimés

### Matériel participant
- [ ] Cahier de notes
- [ ] Support de cours Jour 3
- [ ] Fiches d'exercices
- [ ] Travaux des Jours 1 et 2

### Documents à distribuer
- [ ] Polycopié "Du MCD au MLD"
- [ ] Fiche "Règles de transformation"
- [ ] Exercices Jour 3

---

## ⏰ DÉROULEMENT DÉTAILLÉ

### MATINÉE (9h00 - 12h00)

---

### 🕘 SÉQUENCE 1 : Révision Jour 2 (9h00 - 9h15)

**Durée :** 15 minutes

**Objectif :** Consolider les acquis et clarifier les points restés obscurs

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Rappel des points clés MCD | Exposé | Diaporama |
| 5 min | Correction rapide exercices | Participatif | Tableau |
| 5 min | Questions/Réponses | Participatif | - |

#### Questions de révision
1. Quelles sont les 3 formes normales ?
2. Qu'est-ce qu'une dépendance fonctionnelle ?
3. Comment représente-t-on une association ternaire ?
4. Donnez un exemple d'association réflexive.

---

### 🕘 SÉQUENCE 2 : MCD - Approfondissement (9h15 - 11h00)

**Durée :** 1h45

**Objectif :** Consolider la maîtrise du MCD avec des cas complexes

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 35 min | Étude de cas 1 : Bibliothèque | Travail dirigé | Énoncé |
| 35 min | Étude de cas 2 : Réservation | Travail dirigé | Énoncé |
| 35 min | Application pédagogique | Travail en groupe | Énoncé |

---

#### 📝 ÉTUDE DE CAS 1 : Gestion de Bibliothèque

**Contexte :**
Une bibliothèque universitaire souhaite informatiser la gestion de ses prêts.

**Règles de gestion :**

1. **Ouvrages**
   - Chaque ouvrage possède un numéro ISBN unique
   - Un ouvrage a un titre, un ou plusieurs auteurs, un éditeur, une année d'édition
   - Plusieurs exemplaires peuvent exister pour un même ouvrage
   - Chaque exemplaire a un numéro d'inventaire unique

2. **Adhérents**
   - Un adhérent est identifié par un numéro de carte
   - Il possède un nom, prénom, adresse, téléphone, email
   - Un adhérent peut être étudiant ou enseignant
   - Les étudiants ont une filière, les enseignants ont un grade

3. **Emprunts**
   - Un adhérent peut emprunter jusqu'à 5 ouvrages
   - La durée maximale d'emprunt est de 3 semaines
   - On enregistre la date d'emprunt et la date de retour prévue
   - On note la date de retour effective

4. **Réservations**
   - Si un ouvrage n'est pas disponible, l'adhérent peut le réserver
   - La réservation a une date et un statut

**Travail demandé :**
Réaliser le MCD complet.

**Solution :**
```
┌─────────────────┐                              ┌─────────────────┐
│    OUVRAGE      │          (1,n)               │    AUTEUR       │
├─────────────────┤◄──────────ECRIRE─────────────├─────────────────┤
│ ISBN            │          (1,n)               │ NumAuteur       │
│ Titre           │                              │ NomAuteur       │
│ AnneeEdition    │                              │ PrenomAuteur    │
└────────┬────────┘                              └─────────────────┘
         │
         │ (1,n)
         │
┌────────┴────────┐
│   EXEMPLAIRE    │
├─────────────────┤
│ NumInventaire   │
│ Etat            │
│ DateAcquisition │
└────────┬────────┘
         │
    (0,n)│
         │
┌────────┴────────┐      ┌─────────────────┐
│    EMPRUNT      │      │    ADHERENT     │
├─────────────────┤      ├─────────────────┤
│ DateEmprunt     │(0,n) │ NumCarte        │
│ DateRetourPrevue│◄─────│ Nom             │
│ DateRetourEffec │      │ Prenom          │
└─────────────────┘      │ Adresse         │
                         │ Tel             │
                         │ Email           │
                         └────────┬────────┘
                                  │
                         ┌────────┴────────┐
                         │                 │
                    ┌────┴────┐       ┌────┴────┐
                    │ ETUDIANT│       │ ENSEIGN │
                    ├─────────┤       ├─────────┤
                    │ Filiere │       │ Grade   │
                    └─────────┘       └─────────┘
```

---

#### 📝 ÉTUDE DE CAS 2 : Système de Réservation

**Contexte :**
Un hôtel souhaite gérer ses réservations de chambres.

**Règles de gestion :**

1. **Chambres**
   - Numéro de chambre, type (simple, double, suite), étage, tarif journalier
   - Une chambre peut avoir des équipements (TV, minibar, coffre...)

2. **Clients**
   - Numéro client, nom, prénom, adresse, téléphone, email
   - Type (individuel, entreprise)
   - Les entreprises ont un numéro SIRET et une raison sociale

3. **Réservations**
   - Date d'arrivée prévue, date de départ prévue
   - Nombre de personnes
   - Statut (confirmée, annulée, en cours)

4. **Séjours**
   - Date d'arrivée effective, date de départ effective
   - Montant total, mode de paiement

**Travail demandé :**
Réaliser le MCD complet.

---

#### 📝 APPLICATION PÉDAGOGIQUE : Cas Économie-Gestion

**Contexte :**
Modéliser un système de gestion des notes pour un établissement scolaire.

**Règles de gestion :**
1. Gestion des élèves (nom, prénom, classe)
2. Gestion des matières (code, libellé, coefficient)
3. Gestion des enseignants (nom, prénom, spécialité)
4. Gestion des évaluations (type, date, note sur 20)
5. Un enseignant peut enseigner plusieurs matières
6. Un élève obtient des notes dans différentes matières

**Travail demandé :**
Réaliser le MCD en groupe (3-4 personnes).

---

### ☕ PAUSE CAFÉ (11h00 - 11h15)

---

### 🕚 SÉQUENCE 3 : Modèle MLD - Partie 1 (11h15 - 12h00)

**Durée :** 45 minutes

**Objectif :** Comprendre le passage du MCD au MLD

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 20 min | Principes de transformation | Exposé | Diaporama |
| 15 min | Transformation des entités | Exposé + Démonstration | Diaporama |
| 10 min | Exemples de conversion | Exercice guidé | Tableau |

#### Contenu détaillé

##### A. Introduction au MLD

**Définition :** Le Modèle Logique de Données représente la structure des données dans un formalisme relationnel, indépendamment du SGBD utilisé.

**Position dans Merise :**
```
       MCD                    MLD                    MPD
  ┌───────────┐          ┌───────────┐          ┌───────────┐
  │ Conceptuel│   ───►   │  Logique  │   ───►   │ Physique  │
  │           │   règles │           │   SGBD   │           │
  └───────────┘   transf.└───────────┘          └───────────┘
```

##### B. Vocabulaire comparatif

| MCD | MLD | Définition |
|-----|-----|------------|
| Entité | Table (Relation) | Ensemble d'occurrences |
| Occurrence | Enregistrement (Tuple) | Ligne de la table |
| Propriété | Attribut (Colonne) | Caractéristique |
| Identifiant | Clé primaire | Identifiant unique |

##### C. Règle 1 : Transformation des entités

**Principe :**
- Chaque entité devient une **table**
- L'identifiant devient la **clé primaire**
- Chaque propriété devient un **attribut**

**Exemple :**
```
MCD :                          MLD :
┌───────────────┐              CLIENT (NumClient, Nom, Prenom, Adresse, Tel)
│    CLIENT     │                     └─────────┘
├───────────────┤                     Clé primaire
│ NumClient     │
│ Nom           │
│ Prenom        │
│ Adresse       │
│ Tel           │
└───────────────┘
```

**Notation MLD :**
- Nom de la table en MAJUSCULES
- Clé primaire soulignée ou en première position
- Clé étrangère précédée de # ou suivie de (FK)

##### D. Exercice pratique rapide

**Transformer ces entités en tables :**

1. PRODUIT (RefProd, Designation, PrixHT, QteStock)
2. EMPLOYE (NumEmp, Nom, Prenom, DateEmb, Salaire)

---

### 🍽️ PAUSE DÉJEUNER (12h00 - 13h30)

---

### APRÈS-MIDI (13h30 - 16h30)

---

### 🕜 SÉQUENCE 4 : Modèle MLD - Partie 2 (13h30 - 15h15)

**Durée :** 1h45

**Objectif :** Maîtriser la transformation des associations

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 20 min | Clés primaires et étrangères | Exposé | Diaporama |
| 30 min | Transformation associations 1:N | Exposé + Exercices | Diaporama |
| 30 min | Transformation associations N:N | Exposé + Exercices | Diaporama |
| 25 min | Cas particuliers et optimisation | Exposé + Discussion | Diaporama |

#### Contenu détaillé

##### A. Les Clés

###### Clé Primaire (Primary Key - PK)
- Identifie de façon unique chaque enregistrement
- Ne peut pas être NULL
- Peut être simple ou composée

###### Clé Étrangère (Foreign Key - FK)
- Référence la clé primaire d'une autre table
- Assure l'intégrité référentielle
- Peut être NULL (selon les contraintes)

##### B. Règle 2 : Transformation des associations 1:N (Un à Plusieurs)

**Principe :** La clé primaire du côté "1" migre comme clé étrangère vers le côté "N".

**Exemple :**
```
MCD :
┌───────────┐  (1,1)        (0,n)  ┌───────────┐
│   CLASSE  │───── APPARTENIR ────│   ELEVE   │
├───────────┤                      ├───────────┤
│ CodeClasse│                      │ NumEleve  │
│ Libelle   │                      │ Nom       │
│ Niveau    │                      │ Prenom    │
└───────────┘                      └───────────┘

MLD :
CLASSE (CodeClasse, Libelle, Niveau)
ELEVE (NumEleve, Nom, Prenom, #CodeClasse)
                              └──────────┘
                              Clé étrangère référençant CLASSE
```

**Lecture :** Un élève appartient à UNE classe, une classe a PLUSIEURS élèves.

##### C. Règle 3 : Transformation des associations N:N (Plusieurs à Plusieurs)

**Principe :** L'association devient une TABLE avec :
- Les clés primaires des deux entités comme clé composée
- Les propriétés de l'association comme attributs

**Exemple :**
```
MCD :
┌───────────┐  (0,n)        (1,n)  ┌───────────┐
│   ELEVE   │───── INSCRIPTION ───│   COURS   │
├───────────┤         │           ├───────────┤
│ NumEleve  │     DateInsc        │ CodeCours │
│ Nom       │     Note            │ Intitule  │
└───────────┘                     └───────────┘

MLD :
ELEVE (NumEleve, Nom)
COURS (CodeCours, Intitule)
INSCRIPTION (#NumEleve, #CodeCours, DateInsc, Note)
             └────────────────────┘
             Clé primaire composée (les deux FK)
```

##### D. Règle 4 : Transformation des associations 1:1

**Principe :** La clé primaire d'une entité migre vers l'autre (choix selon les cardinalités).

**Cas (1,1) - (0,1) :** La FK va du côté (1,1)

**Exemple :**
```
MCD :
┌───────────┐  (1,1)        (0,1)  ┌───────────┐
│  EMPLOYE  │───── DIRIGER ───────│  SERVICE  │
├───────────┤                      ├───────────┤
│ NumEmp    │                      │ CodeServ  │
│ Nom       │                      │ LibServ   │
└───────────┘                      └───────────┘

MLD :
SERVICE (CodeServ, LibServ)
EMPLOYE (NumEmp, Nom, #CodeServ)
```

##### E. Règle 5 : Transformation des associations ternaires

**Principe :** L'association devient une table avec les 3 clés primaires.

**Exemple :**
```
MCD :
                    SALLE
                      │
                    (0,n)
                      │
              ┌───────┴───────┐
              │   AFFECTER    │
              │   Horaire     │
              └───────────────┘
             ╱                 ╲
       (1,n)╱                   ╲(1,n)
           ╱                     ╲
       COURS                 PROFESSEUR

MLD :
SALLE (NumSalle, Capacite)
COURS (CodeCours, Intitule)
PROFESSEUR (NumProf, Nom)
AFFECTER (#CodeCours, #NumProf, #NumSalle, Horaire)
          └───────────────────────────────┘
          Clé primaire composée de 3 FK
```

##### F. Règle 6 : Transformation des associations réflexives

**Principe :** Ajouter une clé étrangère qui référence la même table.

**Exemple (hiérarchie) :**
```
MCD :
              ┌───────────────────────┐
              │                       │
   (0,n)      ▼                       │(0,1)
              │                       │
        ┌─────┴─────┐                 │
        │  EMPLOYE  │─────────────────┘
        ├───────────┤    SUPERVISE
        │ NumEmp    │
        │ Nom       │
        └───────────┘

MLD :
EMPLOYE (NumEmp, Nom, #NumEmpSuperviseur)
                      └─────────────────┘
                      FK référençant EMPLOYE.NumEmp (peut être NULL)
```

##### G. Exercice pratique : Transformation complète

**MCD donné :**
```
┌─────────────┐ (1,1)    (0,n) ┌─────────────┐ (1,n)    (1,n) ┌─────────────┐
│ DEPARTEMENT │────APPARTENIR──│   EMPLOYE   │────PARTICIPER──│   PROJET    │
├─────────────┤                ├─────────────┤       │        ├─────────────┤
│ CodeDept    │                │ NumEmp      │   NbHeures     │ NumProjet   │
│ NomDept     │                │ Nom         │                │ Intitule    │
│ Budget      │                │ Salaire     │                │ Budget      │
└─────────────┘                └─────────────┘                └─────────────┘
```

**Travail demandé :** Écrire le MLD correspondant.

**Solution :**
```
DEPARTEMENT (CodeDept, NomDept, Budget)
EMPLOYE (NumEmp, Nom, Salaire, #CodeDept)
PROJET (NumProjet, Intitule, Budget)
PARTICIPER (#NumEmp, #NumProjet, NbHeures)
```

---

### ☕ PAUSE (15h15 - 15h30)

---

### 🕞 SÉQUENCE 5 : Modèle MLD - Partie 3 (15h30 - 16h30)

**Durée :** 1 heure

**Objectif :** Pratiquer la transformation et vérifier la cohérence

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 40 min | Exercice complet MCD → MLD | Travail individuel | Énoncé |
| 15 min | Correction et discussion | Participatif | Tableau |
| 5 min | Synthèse du jour | Exposé | - |

---

#### 📝 EXERCICE COMPLET : Du MCD au MLD

**Reprendre le MCD de la Gestion Commerciale (Jour 2) et réaliser le MLD complet.**

**Rappel du MCD simplifié :**
- CATEGORIE (CodeCat, Libelle) avec sous-catégories
- PRODUIT (RefProd, Designation, PrixHT, QteStock) appartient à CATEGORIE
- PRODUIT peut se composer de PRODUIT
- FOURNISSEUR (CodeFourn, RaisonSoc, Adresse, Tel)
- FOURNISSEUR fournit PRODUIT (avec PrixAchat, Delai)
- CLIENT (NumClient, Nom, Adresse, Tel, Email)
- CLIENT peut être PARTICULIER ou ENTREPRISE (SIRET)
- COMMANDE (NumCmd, DateCmd, Statut) passée par CLIENT
- COMMANDE contient PRODUIT (Quantite, PrixVente)

**Solution MLD :**
```
CATEGORIE (CodeCat, Libelle, #CodeCatParent)

PRODUIT (RefProd, Designation, PrixHT, QteStock, #CodeCat)

COMPOSITION (#RefProdCompose, #RefProdComposant, Quantite)

FOURNISSEUR (CodeFourn, RaisonSoc, Adresse, Tel)

FOURNIR (#RefProd, #CodeFourn, PrixAchat, Delai)

CLIENT (NumClient, Nom, Adresse, Tel, Email, TypeClient)

PARTICULIER (#NumClient, DateNaissance)

ENTREPRISE (#NumClient, SIRET, RaisonSociale)

COMMANDE (NumCmd, DateCmd, Statut, #NumClient)

LIGNE_COMMANDE (#NumCmd, #RefProd, Quantite, PrixVente)
```

---

#### 📋 Dictionnaire des Données

| Table | Attribut | Type | Taille | Contraintes | Description |
|-------|----------|------|--------|-------------|-------------|
| CATEGORIE | CodeCat | CHAR | 5 | PK | Code catégorie |
| CATEGORIE | Libelle | VARCHAR | 50 | NOT NULL | Libellé catégorie |
| CATEGORIE | CodeCatParent | CHAR | 5 | FK, NULL | Catégorie parente |
| PRODUIT | RefProd | CHAR | 10 | PK | Référence produit |
| PRODUIT | Designation | VARCHAR | 100 | NOT NULL | Désignation |
| PRODUIT | PrixHT | DECIMAL | 10,2 | NOT NULL | Prix HT |
| PRODUIT | QteStock | INT | - | >= 0 | Quantité en stock |
| PRODUIT | CodeCat | CHAR | 5 | FK, NOT NULL | Catégorie |

---

## ✅ SYNTHÈSE DU JOUR 3

### Règles de transformation résumées

| Type d'association | Transformation |
|--------------------|----------------|
| Entité | → Table avec clé primaire |
| Association 1:N | → FK du côté N |
| Association N:N | → Table intermédiaire avec clé composée |
| Association 1:1 | → FK du côté (1,1) |
| Association ternaire | → Table avec 3 FK en clé composée |
| Association réflexive | → FK vers même table |

### Points clés à retenir

| Concept | Définition |
|---------|------------|
| **MLD** | Modèle relationnel indépendant du SGBD |
| **Table** | Ensemble structuré d'enregistrements |
| **Clé primaire** | Identifiant unique d'un enregistrement |
| **Clé étrangère** | Référence vers clé primaire d'une autre table |
| **Intégrité référentielle** | Cohérence des références entre tables |

### Préparation Jour 4
- Revoir le MLD créé
- Se préparer à l'implémentation physique
- Avoir Access installé sur son poste

---

## 📊 ÉVALUATION DE LA SÉANCE

### Grille d'observation formateur

| Critère | Non acquis | En cours | Acquis |
|---------|------------|----------|--------|
| Cas complexes MCD | ☐ | ☐ | ☐ |
| Règles de transformation | ☐ | ☐ | ☐ |
| Transformation 1:N | ☐ | ☐ | ☐ |
| Transformation N:N | ☐ | ☐ | ☐ |
| Transformation réflexive | ☐ | ☐ | ☐ |
| Vérification cohérence | ☐ | ☐ | ☐ |

### Auto-évaluation participant

1. Je maîtrise les cas complexes de MCD : ☐ Oui ☐ Partiellement ☐ Non
2. Je sais transformer un MCD en MLD : ☐ Oui ☐ Partiellement ☐ Non
3. Je comprends les clés étrangères : ☐ Oui ☐ Partiellement ☐ Non

---

## 📎 DOCUMENTS ANNEXES JOUR 3

- Annexe 3A : Diaporama "Du MCD au MLD"
- Annexe 3B : Fiche "Règles de transformation"
- Annexe 3C : Exercices et corrigés Jour 3
- Annexe 3D : Études de cas détaillées
