# Jour 1 - Introduction à Merise et Modélisation E/A

## Durée : 6 heures

---

## Planning de la Journée

### Matinée (9h00 - 12h00) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 9h00 - 9h15 | Accueil et Introduction | Présentation des participants, Objectifs, Programme | 15min |
| 9h15 - 10h15 | Présentation générale et Notion SGBD | Introduction à Merise, Histoire, SGBD | 1h |
| 10h15 - 10h30 | PAUSE CAFÉ | | 15min |
| 10h30 - 12h00 | Modèle E/A - Partie 1 | Entités, Attributs, Propriétés | 1h30 |

### Après-midi (13h30 - 16h30) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 13h30 - 15h15 | Modèle E/A - Partie 2 | Relations, Cardinalités, Types de relations | 1h45 |
| 15h15 - 15h30 | PAUSE | | 15min |
| 15h30 - 16h30 | Modèle E/A - Partie 3 | Exercices pratiques, Études de cas | 1h |

---

## Module 1 : Accueil et Introduction (15 min)

### Objectifs
- Créer un environnement d'apprentissage collaboratif
- Présenter les objectifs de la formation
- Établir les règles de fonctionnement

### Activité : Tour de Table
Chaque participant se présente en 1 minute :
- Nom et établissement
- Matières enseignées
- Attentes vis-à-vis de la formation
- Niveau de familiarité avec les bases de données

---

## Module 2 : Présentation Générale et Notion SGBD (1h)

### 2.1 Introduction à la Méthode Merise

#### Définition
Merise est une **méthode d'analyse, de conception et de gestion de projet informatique** développée en France dans les années 1970-1980. Elle est particulièrement adaptée aux systèmes d'information de gestion.

#### Historique
- **1974** : Naissance du projet Merise au ministère de l'Industrie
- **1978** : Publication officielle de la méthode
- **1980s** : Adoption massive dans les entreprises françaises
- **Aujourd'hui** : Reste une référence pour la modélisation de bases de données

#### Les Trois Niveaux de Merise

```
┌─────────────────────────────────────────────┐
│           NIVEAU CONCEPTUEL                 │
│         (MCD, MCT, MOT)                     │
│         "QUOI ?" - Les données              │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│            NIVEAU LOGIQUE                   │
│              (MLD)                          │
│        "COMMENT ?" - L'organisation         │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│           NIVEAU PHYSIQUE                   │
│              (MPD)                          │
│       "AVEC QUOI ?" - L'implémentation      │
└─────────────────────────────────────────────┘
```

### 2.2 Systèmes de Gestion de Bases de Données (SGBD)

#### Définition
Un SGBD est un **logiciel permettant de stocker, organiser, gérer et interroger** de grandes quantités de données de manière efficace et sécurisée.

#### Fonctionnalités principales
1. **Définition des données** : Structure, types, contraintes
2. **Manipulation des données** : Ajout, modification, suppression, recherche
3. **Contrôle d'accès** : Sécurité, droits utilisateurs
4. **Intégrité des données** : Cohérence, validité
5. **Gestion des transactions** : ACID (Atomicité, Cohérence, Isolation, Durabilité)

#### Types de SGBD

| Type | Exemples | Caractéristiques |
|------|----------|------------------|
| Relationnel | MySQL, PostgreSQL, MS Access, Oracle | Tables, relations, SQL |
| NoSQL | MongoDB, Cassandra | Documents, flexibilité |
| Hiérarchique | IMS | Arborescence |
| Réseau | IDMS | Graphes |

#### Importance dans l'Enseignement
- **Compétences numériques** : Préparation aux métiers du numérique
- **Gestion de l'information** : Organisation structurée des données
- **Applications pratiques** : Projets concrets en économie-gestion
- **Programmes officiels** : Intégration dans les référentiels

### Activité 1.1 : Réflexion Collective
**Durée : 10 minutes**

En petits groupes, identifiez des exemples de bases de données utilisées dans :
1. Votre établissement scolaire
2. La vie quotidienne
3. Le monde de l'entreprise

**Partage en plénière** : Discussion sur les caractéristiques communes

---

## Module 3 : Modèle E/A - Partie 1 (1h30)

### 3.1 Concepts Fondamentaux

#### L'Entité

**Définition** : Une entité est un **objet du monde réel** ayant une existence propre et que l'on souhaite gérer dans le système d'information.

**Représentation graphique** :
```
┌─────────────────┐
│     ENTITÉ      │
├─────────────────┤
│ propriété1      │
│ propriété2      │
│ propriété3      │
└─────────────────┘
```

**Exemples d'entités** :
- ETUDIANT
- PROFESSEUR
- COURS
- PRODUIT
- CLIENT
- COMMANDE

#### Les Attributs (ou Propriétés)

**Définition** : Un attribut est une **caractéristique** qui décrit une entité.

**Types d'attributs** :
1. **Simple** : Valeur unique (ex: Nom)
2. **Composé** : Plusieurs composants (ex: Adresse = Rue + Ville + Code Postal)
3. **Dérivé** : Calculé à partir d'autres attributs (ex: Âge calculé depuis Date de Naissance)
4. **Multivalué** : Plusieurs valeurs possibles (ex: Téléphones)

#### L'Identifiant (Clé Primaire)

**Définition** : L'identifiant est un **attribut ou ensemble d'attributs** qui permet d'identifier de manière unique chaque occurrence d'une entité.

**Caractéristiques** :
- Unique pour chaque occurrence
- Non null (obligatoire)
- Stable dans le temps
- Souligné dans la représentation graphique

**Exemple** :
```
┌─────────────────────────┐
│        ETUDIANT         │
├─────────────────────────┤
│ NumeroEtudiant (PK)     │
│ Nom                     │
│ Prenom                  │
│ DateNaissance           │
│ Email                   │
└─────────────────────────┘
```

### 3.2 Exemples Détaillés

#### Exemple 1 : Gestion d'Étudiants

```
┌─────────────────────────┐
│        ETUDIANT         │
├─────────────────────────┤
│ NumEtudiant (PK)        │
│ Nom                     │
│ Prenom                  │
│ DateNaissance           │
│ Adresse                 │
│ Email                   │
│ Telephone               │
└─────────────────────────┘

┌─────────────────────────┐
│         CLASSE          │
├─────────────────────────┤
│ CodeClasse (PK)         │
│ NomClasse               │
│ Niveau                  │
│ Effectif                │
└─────────────────────────┘
```

#### Exemple 2 : Gestion de Stock

```
┌─────────────────────────┐
│        PRODUIT          │
├─────────────────────────┤
│ RefProduit (PK)         │
│ Designation             │
│ PrixUnitaire            │
│ QuantiteStock           │
│ SeuilAlerte             │
└─────────────────────────┘

┌─────────────────────────┐
│       FOURNISSEUR       │
├─────────────────────────┤
│ CodeFournisseur (PK)    │
│ RaisonSociale           │
│ Adresse                 │
│ Telephone               │
│ Email                   │
└─────────────────────────┘
```

### Activité 1.2 : Identification d'Entités
**Durée : 20 minutes**

**Exercice** : Pour chacun des cas suivants, identifiez les entités et leurs attributs :

1. **Bibliothèque scolaire**
   - Gérer les livres, les emprunts et les adhérents

2. **Cantine scolaire**
   - Gérer les repas, les élèves et les inscriptions

3. **Club sportif**
   - Gérer les membres, les activités et les inscriptions

**Format de réponse** :
```
ENTITÉ : [Nom]
Attributs :
- Identifiant : [nom_attribut]
- [attribut1]
- [attribut2]
- ...
```

---

## Module 4 : Modèle E/A - Partie 2 (1h45)

### 4.1 Relations et Associations

#### Définition
Une **relation** (ou association) représente un **lien sémantique** entre deux ou plusieurs entités.

**Représentation graphique** :
```
┌──────────┐          ┌──────────┐
│ ENTITÉ A │──────────│ ENTITÉ B │
└──────────┘    ▲     └──────────┘
                │
           ┌────┴────┐
           │ RELATION│
           └─────────┘
```

#### Types de Relations

1. **Relation binaire** : Entre 2 entités
2. **Relation ternaire** : Entre 3 entités
3. **Relation réflexive** : Une entité avec elle-même

### 4.2 Cardinalités

#### Définition
La **cardinalité** exprime le **nombre minimum et maximum** d'occurrences d'une entité pouvant participer à une relation.

#### Notation
**[min, max]** ou **(min, max)**

| Cardinalité | Signification |
|-------------|---------------|
| 0,1 | Aucune ou une seule occurrence |
| 1,1 | Une et une seule occurrence |
| 0,n | Aucune ou plusieurs occurrences |
| 1,n | Une ou plusieurs occurrences |

#### Types de Relations selon les Cardinalités

**1. Relation Un à Un (1:1)**
```
┌──────────┐  1,1      1,1  ┌──────────┐
│ PERSONNE │────────────────│ PASSPORT │
└──────────┘                └──────────┘
```
*Une personne possède un et un seul passeport ; un passeport appartient à une et une seule personne.*

**2. Relation Un à Plusieurs (1:N)**
```
┌──────────┐  1,n      1,1  ┌──────────┐
│  CLASSE  │────────────────│ ETUDIANT │
└──────────┘                └──────────┘
```
*Une classe contient plusieurs étudiants ; un étudiant appartient à une seule classe.*

**3. Relation Plusieurs à Plusieurs (N:M)**
```
┌──────────┐  0,n      0,n  ┌──────────┐
│ ETUDIANT │────────────────│  COURS   │
└──────────┘                └──────────┘
```
*Un étudiant peut s'inscrire à plusieurs cours ; un cours peut avoir plusieurs étudiants.*

### 4.3 Exemples Complets

#### Exemple : Système de Gestion Scolaire

```
                            ENSEIGNE
                         ┌───────────┐
                         │  Matiere  │
                         │  Horaire  │
                         └─────┬─────┘
                               │
┌─────────────┐  1,n      0,n  │  0,n      1,1  ┌─────────────┐
│ PROFESSEUR  │────────────────┼────────────────│   CLASSE    │
├─────────────┤                │                ├─────────────┤
│ NumProf(PK) │                │                │ CodeClasse  │
│ Nom         │                │                │ NomClasse   │
│ Prenom      │                │                │ Niveau      │
│ Specialite  │                │                └──────┬──────┘
└─────────────┘                │                       │
                               │                       │ 1,n
                               │                       │
                               │                ┌──────┴──────┐
                               │                │  ETUDIANT   │
                               │                ├─────────────┤
                               └────────────────│ NumEtud(PK) │
                                       0,n      │ Nom         │
                                                │ Prenom      │
                                                │ DateNaiss   │
                                                └─────────────┘
```

### 4.4 Contraintes sur les Relations

#### Contrainte d'Intégrité Référentielle
Garantit que toute référence à une entité pointe vers une occurrence existante.

#### Contrainte de Participation
- **Participation totale** : Chaque occurrence doit participer à la relation (min ≥ 1)
- **Participation partielle** : Une occurrence peut ne pas participer (min = 0)

### Activité 1.3 : Cardinalités
**Durée : 25 minutes**

**Exercice** : Déterminez les cardinalités pour les relations suivantes :

1. AUTEUR écrit LIVRE
2. PATIENT consulte MEDECIN
3. EMPLOYE travaille_dans DEPARTEMENT
4. COMMANDE contient PRODUIT
5. ELEVE emprunte LIVRE

**Format de réponse** :
```
ENTITÉ1 (card1,card2) ──RELATION── (card3,card4) ENTITÉ2
```

---

## Module 5 : Modèle E/A - Partie 3 (1h)

### 5.1 Études de Cas Pratiques

#### Cas 1 : Gestion des Étudiants

**Contexte** : Un établissement scolaire souhaite gérer les informations suivantes :
- Les étudiants et leurs informations personnelles
- Les classes et leur composition
- Les professeurs et leurs affectations
- Les matières enseignées

**Travail demandé** :
1. Identifier les entités
2. Définir les attributs de chaque entité
3. Établir les relations avec les cardinalités

**Solution attendue** :
```
┌─────────────┐              ┌─────────────┐
│  ETUDIANT   │              │   CLASSE    │
├─────────────┤              ├─────────────┤
│ NumEtud(PK) │    1,1  0,n  │ CodeClasse  │
│ Nom         │──────────────│ Libelle     │
│ Prenom      │  appartient  │ Niveau      │
│ DateNaiss   │              │ Annee       │
│ Adresse     │              └──────┬──────┘
└─────────────┘                     │
                                    │ 0,n
                              ┌─────┴─────┐
                              │  AFFECTE  │
                              │ NbHeures  │
                              └─────┬─────┘
                                    │
┌─────────────┐    0,n        1,n   │
│ PROFESSEUR  │─────────────────────┘
├─────────────┤    enseigne
│ NumProf(PK) │
│ Nom         │
│ Prenom      │
│ Grade       │
│ Specialite  │
└─────────────┘
```

#### Cas 2 : Gestion de Stock

**Contexte** : Une entreprise commerciale gère :
- Un catalogue de produits
- Les fournisseurs
- Les commandes passées aux fournisseurs
- Le stock disponible

**Travail demandé** :
1. Modéliser le système avec le modèle E/A
2. Inclure les attributs pertinents
3. Vérifier la cohérence des cardinalités

### 5.2 Correction Collective

**Méthodologie de correction** :
1. Présentation des solutions par groupe
2. Discussion des choix de modélisation
3. Identification des erreurs courantes
4. Validation du modèle final

### Activité 1.4 : Projet de Fin de Journée
**Durée : 30 minutes**

**Consigne** : En binôme, modélisez le système d'information suivant :

**Cas : Association Sportive**

L'association gère :
- Des membres (nom, prénom, date d'inscription, cotisation)
- Des activités sportives (nom, jour, horaire, lieu)
- Des inscriptions des membres aux activités
- Des encadrants (professeurs/moniteurs)

**Livrables attendus** :
1. Liste des entités avec leurs attributs
2. Liste des relations avec leurs cardinalités
3. Schéma E/A complet

---

## Synthèse de la Journée

### Points Clés à Retenir

1. **Merise** est une méthode structurée de conception de systèmes d'information
2. **L'entité** représente un objet du monde réel avec des attributs
3. **L'identifiant** permet de distinguer chaque occurrence de manière unique
4. **Les relations** lient les entités entre elles
5. **Les cardinalités** précisent les règles de participation aux relations

### Vocabulaire Essentiel

| Terme | Définition |
|-------|------------|
| Entité | Objet du monde réel à gérer |
| Attribut | Propriété caractérisant une entité |
| Identifiant | Attribut unique identifiant une occurrence |
| Relation | Lien sémantique entre entités |
| Cardinalité | Nombre min/max de participations |
| SGBD | Logiciel de gestion de bases de données |

### Préparation pour le Jour 2

**À réviser** :
- Les concepts d'entité et d'attribut
- Les différents types de cardinalités
- La lecture d'un schéma E/A

**Questions de réflexion** :
1. Quelles différences voyez-vous entre un schéma E/A et une liste de tables ?
2. Comment utiliseriez-vous ces concepts avec vos élèves ?

---

## Ressources Complémentaires

- [Exercices supplémentaires - Jour 1](./activites/exercices_jour1.md)
- [Corrigés des exercices](./corriges/corriges_jour1.md)
