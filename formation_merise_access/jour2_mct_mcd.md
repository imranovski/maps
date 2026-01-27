# Jour 2 - MCT et Modèle Conceptuel de Données (MCD)

## Durée : 6 heures

---

## Planning de la Journée

### Matinée (9h00 - 12h00) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 9h00 - 9h15 | Révision Jour 1 | Rappel Modèle E/A, Questions/Réponses | 15min |
| 9h15 - 10h15 | Modèle MCT | Événements, Opérations, Processus métier | 1h |
| 10h15 - 10h30 | PAUSE CAFÉ | | 15min |
| 10h30 - 12h00 | Modèle MCD - Partie 1 | Formalisme, Normalisation, Dépendances | 1h30 |

### Après-midi (13h30 - 16h30) - 3h

| Horaire | Module | Contenu | Durée |
|---------|--------|---------|-------|
| 13h30 - 15h15 | Modèle MCD - Partie 2 | Entités avancées, Relations ternaires | 1h45 |
| 15h15 - 15h30 | PAUSE | | 15min |
| 15h30 - 16h30 | Modèle MCD - Partie 3 | Études de cas, Travail en groupe | 1h |

---

## Module 1 : Révision Jour 1 (15 min)

### Quiz Rapide

1. Qu'est-ce qu'une entité ?
2. À quoi sert un identifiant ?
3. Que signifie la cardinalité (1,n) ?
4. Quelle est la différence entre une relation 1:1 et 1:N ?

### Correction des Exercices

Discussion sur les difficultés rencontrées lors des exercices du Jour 1.

---

## Module 2 : Modèle Conceptuel des Traitements (MCT) (1h)

### 2.1 Introduction au MCT

#### Définition
Le **Modèle Conceptuel des Traitements (MCT)** décrit les traitements effectués sur les données en réponse à des événements, indépendamment de toute considération technique.

#### Objectif
Représenter le **"QUOI"** des traitements : quels traitements sont déclenchés par quels événements ?

### 2.2 Composants du MCT

#### Les Événements

**Définition** : Un événement est un **fait déclencheur** qui provoque l'exécution d'une opération.

**Types d'événements** :
1. **Événement externe** : Provient de l'extérieur du système
2. **Événement interne** : Résultat d'une opération précédente
3. **Événement temporel** : Lié à une condition de temps

**Représentation** :
```
    ╭─────────────╮
    │  Événement  │
    ╰─────────────╯
```

#### La Synchronisation

**Définition** : La synchronisation définit les **conditions logiques** de déclenchement d'une opération.

**Opérateurs** :
- **ET** : Tous les événements doivent être présents
- **OU** : Au moins un événement doit être présent

**Représentation** :
```
    ╭─────────╮     ╭─────────╮
    │ Évént 1 │     │ Évént 2 │
    ╰────┬────╯     ╰────┬────╯
         │     ET       │
         └──────┬───────┘
                ↓
```

#### Les Opérations

**Définition** : Une opération est un **ensemble de traitements** exécutés de manière ininterruptible.

**Caractéristiques** :
- Déclenchée par un ou plusieurs événements
- Produit un ou plusieurs résultats
- Atomique (tout ou rien)

**Représentation** :
```
┌─────────────────────────────────────┐
│            OPÉRATION                │
├─────────────────────────────────────┤
│  - Action 1                         │
│  - Action 2                         │
│  - Action 3                         │
├─────────────────────────────────────┤
│  Règles d'émission :                │
│  Condition 1 → Résultat 1           │
│  Condition 2 → Résultat 2           │
└─────────────────────────────────────┘
```

#### Les Résultats

**Définition** : Un résultat est un **événement produit** par une opération.

**Types** :
- Résultat positif (succès)
- Résultat négatif (échec)

### 2.3 Exemple Complet : Processus de Commande

```
    ╭──────────────────╮
    │ Demande Client   │
    ╰────────┬─────────╯
             │
             ↓
┌────────────────────────────────────────┐
│        VERIFIER DISPONIBILITE          │
├────────────────────────────────────────┤
│  - Consulter le stock                  │
│  - Vérifier la quantité demandée       │
├────────────────────────────────────────┤
│  Toujours → Stock vérifié              │
└────────────────────────────────────────┘
             │
    ╭────────┴────────╮
    │  Stock vérifié  │
    ╰────────┬────────╯
             │
             ↓
┌────────────────────────────────────────┐
│         TRAITER COMMANDE               │
├────────────────────────────────────────┤
│  - Créer la commande                   │
│  - Mettre à jour le stock              │
│  - Calculer le montant                 │
├────────────────────────────────────────┤
│  Stock suffisant → Commande validée    │
│  Stock insuffisant → Commande refusée  │
└────────────────────────────────────────┘
          /             \
    ╭────┴───╮      ╭────┴──────╮
    │Commande│      │ Commande  │
    │validée │      │ refusée   │
    ╰────────╯      ╰───────────╯
```

### Activité 2.1 : Création d'un MCT
**Durée : 20 minutes**

**Exercice** : Modélisez le processus suivant avec un MCT :

**Inscription d'un étudiant à un cours** :
1. L'étudiant fait une demande d'inscription
2. Le secrétariat vérifie les prérequis
3. Si les prérequis sont validés, l'inscription est enregistrée
4. Sinon, la demande est refusée

---

## Module 3 : Modèle MCD - Partie 1 (1h30)

### 3.1 Formalisme du MCD

#### Définition
Le **Modèle Conceptuel de Données (MCD)** est une représentation structurée des données et de leurs relations, indépendante de toute implémentation technique.

#### Composants du MCD

**1. Les Entités**
```
┌─────────────────────┐
│      ENTITÉ         │
├─────────────────────┤
│ identifiant (PK)    │
│ attribut1           │
│ attribut2           │
└─────────────────────┘
```

**2. Les Associations**
```
┌──────────┐           ┌──────────┐
│ ENTITÉ A │───────────│ ENTITÉ B │
└──────────┘     │     └──────────┘
            ┌───┴───┐
            │ASSOC  │
            │attr   │
            └───────┘
```

**3. Les Cardinalités**
Notées sur chaque branche de l'association

### 3.2 Règles de Normalisation

#### Objectifs de la Normalisation
- Éliminer la **redondance** des données
- Éviter les **anomalies** de mise à jour
- Assurer l'**intégrité** des données

#### Première Forme Normale (1FN)

**Règle** : Chaque attribut doit contenir une **valeur atomique** (indivisible).

**Exemple NON 1FN** :
```
ETUDIANT
│ NumEtud │ Nom    │ Telephones          │
│ 001     │ Dupont │ 0612345678, 0698765432 │
```

**Correction 1FN** :
```
ETUDIANT                    TELEPHONE
│ NumEtud │ Nom    │        │ NumEtud │ Numero     │
│ 001     │ Dupont │        │ 001     │ 0612345678 │
                            │ 001     │ 0698765432 │
```

#### Deuxième Forme Normale (2FN)

**Règle** : Être en 1FN ET chaque attribut non-clé doit dépendre de **toute la clé primaire**.

**Exemple NON 2FN** :
```
INSCRIPTION (NumEtud, CodeCours, Note, NomEtud)
                                      ↑
                    Dépend uniquement de NumEtud, pas de la clé entière
```

**Correction 2FN** :
```
ETUDIANT (NumEtud, NomEtud)
INSCRIPTION (NumEtud, CodeCours, Note)
```

#### Troisième Forme Normale (3FN)

**Règle** : Être en 2FN ET aucun attribut non-clé ne doit dépendre d'un autre attribut non-clé.

**Exemple NON 3FN** :
```
ETUDIANT (NumEtud, Nom, CodeDepartement, NomDepartement)
                              ↓              ↓
              NomDepartement dépend de CodeDepartement
```

**Correction 3FN** :
```
ETUDIANT (NumEtud, Nom, CodeDepartement)
DEPARTEMENT (CodeDepartement, NomDepartement)
```

### 3.3 Dépendances Fonctionnelles

#### Définition
Une **dépendance fonctionnelle (DF)** existe lorsqu'un attribut A détermine de manière unique un attribut B.

**Notation** : A → B (A détermine B)

#### Exemples
- NumEtud → NomEtud (Le numéro étudiant détermine le nom)
- ISBN → TitreLivre (L'ISBN détermine le titre)
- (NumCommande, RefProduit) → Quantité (La combinaison détermine la quantité)

#### Types de Dépendances

1. **DF Élémentaire** : A → B où B ne dépend pas d'une partie de A
2. **DF Directe** : A → B sans intermédiaire
3. **DF Transitive** : A → B et B → C implique A → C

### Activité 2.2 : Normalisation
**Durée : 25 minutes**

**Exercice 1** : Identifiez la forme normale et corrigez si nécessaire :

```
COMMANDE
│ NumCmd │ DateCmd │ NumClient │ NomClient │ Adresse │ Produits        │
│ 001    │ 15/01   │ C001      │ Martin    │ Paris   │ P1:2, P2:5, P3:1│
```

**Exercice 2** : Identifiez les dépendances fonctionnelles :

```
FACTURE (NumFacture, DateFacture, NumClient, NomClient, MontantTotal)
```

---

## Module 4 : Modèle MCD - Partie 2 (1h45)

### 4.1 Entités et Relations Avancées

#### Entité Faible

**Définition** : Une entité dont l'existence dépend d'une autre entité (entité forte).

**Caractéristiques** :
- Ne peut pas exister sans l'entité forte
- Son identifiant inclut celui de l'entité forte

**Exemple** :
```
┌─────────────┐  1,n        1,1  ┌─────────────┐
│   COMMANDE  │──────────────────│    LIGNE    │
│             │   contient       │  COMMANDE   │
├─────────────┤                  ├─────────────┤
│ NumCmd (PK) │                  │ NumLigne    │
│ DateCmd     │                  │ Quantite    │
│ MontantTotal│                  │ PrixUnit    │
└─────────────┘                  └─────────────┘
                                 Identifiant: (NumCmd, NumLigne)
```

#### Spécialisation / Généralisation

**Définition** : Relation d'héritage entre entités.

**Représentation** :
```
              ┌─────────────┐
              │   PERSONNE  │
              ├─────────────┤
              │ NumPers (PK)│
              │ Nom         │
              │ Prenom      │
              └──────┬──────┘
                     │
            ┌────────┴────────┐
            │                 │
     ┌──────┴──────┐   ┌──────┴──────┐
     │  ETUDIANT   │   │ PROFESSEUR  │
     ├─────────────┤   ├─────────────┤
     │ NumEtud     │   │ NumProf     │
     │ Niveau      │   │ Grade       │
     │ Filiere     │   │ Specialite  │
     └─────────────┘   └─────────────┘
```

### 4.2 Relations Ternaires

**Définition** : Une relation ternaire implique **trois entités** simultanément.

**Exemple : Enseignement**

Un professeur enseigne une matière dans une classe.

```
┌─────────────┐
│ PROFESSEUR  │
├─────────────┤
│ NumProf(PK) │──────────┐
│ Nom         │          │
└─────────────┘          │ 0,n
                         │
                    ┌────┴────┐
                    │ENSEIGNE │
                    │ NbHeures│
                    └────┬────┘
                    /         \
              0,n  /           \  0,n
                  /             \
    ┌─────────────┐           ┌─────────────┐
    │   MATIERE   │           │   CLASSE    │
    ├─────────────┤           ├─────────────┤
    │ CodeMat(PK) │           │ CodeCl(PK)  │
    │ Libelle     │           │ Niveau      │
    └─────────────┘           └─────────────┘
```

**Interprétation** : La relation ENSEIGNE lie un professeur, une matière et une classe. L'attribut NbHeures caractérise cette relation ternaire.

### 4.3 Associations Réflexives

**Définition** : Une association réflexive lie une entité **avec elle-même**.

**Exemple 1 : Hiérarchie d'employés**
```
┌─────────────┐
│   EMPLOYE   │
├─────────────┤
│ NumEmp (PK) │◄──────┐
│ Nom         │       │ dirige
│ Prenom      │───────┘
│ Poste       │   0,n      0,1
└─────────────┘
```
*Un employé peut diriger plusieurs employés. Un employé est dirigé par au maximum un autre employé.*

**Exemple 2 : Prérequis de cours**
```
┌─────────────┐
│    COURS    │
├─────────────┤
│ CodeCours   │◄──────┐
│ Intitule    │       │ prerequis_de
│ Credits     │───────┘
└─────────────┘   0,n      0,n
```
*Un cours peut avoir plusieurs prérequis. Un cours peut être prérequis de plusieurs autres cours.*

### 4.4 Cas Complexes

#### Historisation des Données

**Problème** : Comment conserver l'historique des modifications ?

**Solution** : Ajouter une dimension temporelle

```
┌─────────────┐  1,n              0,n  ┌─────────────┐
│   EMPLOYE   │────────────────────────│   SERVICE   │
├─────────────┤     AFFECTATION        ├─────────────┤
│ NumEmp (PK) │     DateDebut          │ CodeServ(PK)│
│ Nom         │     DateFin            │ NomService  │
└─────────────┘                        └─────────────┘
```

#### Attributs sur les Relations

Les relations peuvent porter des attributs propres.

```
┌─────────────┐  0,n          0,n  ┌─────────────┐
│  ETUDIANT   │────────────────────│    COURS    │
├─────────────┤    INSCRIPTION     ├─────────────┤
│ NumEtud(PK) │    DateInscr       │ CodeCours   │
│ Nom         │    Note            │ Intitule    │
└─────────────┘    Appreciation    └─────────────┘
```

### Activité 2.3 : Modélisation Avancée
**Durée : 30 minutes**

**Exercice** : Modélisez les situations suivantes :

1. **Gestion d'un réseau social**
   - Un utilisateur peut suivre d'autres utilisateurs
   - Un utilisateur peut créer des publications
   - Un utilisateur peut commenter des publications

2. **Système de réservation hôtelière**
   - Les clients réservent des chambres
   - Les chambres appartiennent à des hôtels
   - Une réservation a une date de début et de fin

---

## Module 5 : Modèle MCD - Partie 3 (1h)

### 5.1 Étude de Cas : Système de Gestion Commerciale

#### Contexte

Une entreprise commerciale souhaite informatiser sa gestion. Le système doit gérer :

- **Les clients** : Numéro, raison sociale, adresse, téléphone, email
- **Les produits** : Référence, désignation, prix unitaire HT, taux TVA, stock
- **Les fournisseurs** : Code, nom, adresse, conditions de paiement
- **Les commandes clients** : Numéro, date, client, produits commandés avec quantités
- **Les livraisons** : Numéro, date, commande livrée
- **Les factures** : Numéro, date, commande facturée, montant

#### Travail en Groupe

**Phase 1 : Identification des entités (10 min)**
- Listez toutes les entités
- Définissez les attributs de chaque entité
- Identifiez les clés primaires

**Phase 2 : Définition des relations (15 min)**
- Identifiez les relations entre entités
- Déterminez les cardinalités
- Ajoutez les attributs des relations si nécessaire

**Phase 3 : Construction du MCD (20 min)**
- Dessinez le schéma MCD complet
- Vérifiez la cohérence
- Préparez la présentation

**Phase 4 : Présentation et Discussion (15 min)**
- Chaque groupe présente son MCD
- Discussion collective sur les choix
- Correction et amélioration

### 5.2 Solution Proposée

```
┌─────────────────┐                           ┌─────────────────┐
│     CLIENT      │                           │   FOURNISSEUR   │
├─────────────────┤                           ├─────────────────┤
│ NumClient (PK)  │                           │ CodeFourn (PK)  │
│ RaisonSociale   │                           │ NomFourn        │
│ Adresse         │                           │ AdresseFourn    │
│ Telephone       │                           │ CondPaiement    │
│ Email           │                           └────────┬────────┘
└────────┬────────┘                                    │
         │ 1,n                                         │ 1,n
         │                                             │
    ┌────┴────┐                                   ┌────┴────┐
    │  passe  │                                   │ fournit │
    └────┬────┘                                   └────┬────┘
         │ 0,n                                         │ 0,n
         │                                             │
┌────────┴────────┐                           ┌────────┴────────┐
│    COMMANDE     │                           │     PRODUIT     │
├─────────────────┤                           ├─────────────────┤
│ NumCommande(PK) │                           │ RefProduit (PK) │
│ DateCommande    │                           │ Designation     │
│ Statut          │◄──────────────────────────│ PrixUnitHT      │
└────────┬────────┘   0,n  contient   0,n     │ TauxTVA         │
         │                 Quantite           │ StockActuel     │
         │                                    └─────────────────┘
         │ 1,1
         │
    ┌────┴────┐          ┌─────────────────┐
    │ genere  │──────────│     FACTURE     │
    └────┬────┘   0,1    ├─────────────────┤
         │               │ NumFacture (PK) │
         │               │ DateFacture     │
         │               │ MontantHT       │
         │               │ MontantTTC      │
         │               └─────────────────┘
         │ 0,1
         │
    ┌────┴────┐          ┌─────────────────┐
    │concerne │──────────│    LIVRAISON    │
    └─────────┘   0,n    ├─────────────────┤
                         │ NumLivraison(PK)│
                         │ DateLivraison   │
                         │ Statut          │
                         └─────────────────┘
```

---

## Synthèse de la Journée

### Points Clés à Retenir

1. **MCT** modélise les traitements : événements → opérations → résultats
2. **MCD** représente les données et leurs relations de manière conceptuelle
3. **Normalisation** (1FN, 2FN, 3FN) élimine les redondances
4. **Dépendances fonctionnelles** aident à structurer les données
5. **Relations avancées** : ternaires, réflexives, spécialisation

### Vocabulaire du Jour

| Terme | Définition |
|-------|------------|
| MCT | Modèle Conceptuel des Traitements |
| MCD | Modèle Conceptuel de Données |
| Normalisation | Processus d'optimisation de la structure |
| 1FN/2FN/3FN | Formes normales de la base de données |
| DF | Dépendance fonctionnelle |
| Relation ternaire | Association impliquant trois entités |
| Association réflexive | Entité en relation avec elle-même |

### Préparation pour le Jour 3

**À réviser** :
- Les règles de normalisation
- La construction d'un MCD complet
- Les différents types de relations

**Questions de réflexion** :
1. Comment expliquer la normalisation à vos élèves ?
2. Quels cas d'usage pédagogiques pouvez-vous imaginer ?

---

## Ressources Complémentaires

- [Exercices supplémentaires - Jour 2](./activites/exercices_jour2.md)
- [Corrigés des exercices](./corriges/corriges_jour2.md)
