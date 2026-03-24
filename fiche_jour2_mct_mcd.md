# FICHE DE DÉROULEMENT - JOUR 2
## MCT et Modèle Conceptuel de Données (MCD)

---

## 📋 INFORMATIONS DE LA SÉANCE

| Élément | Description |
|---------|-------------|
| **Jour** | Jour 2 sur 5 |
| **Durée** | 6 heures |
| **Thème** | MCT et Modèle Conceptuel de Données (MCD) |
| **Public** | Professeurs d'Économie et Gestion |
| **Niveau** | Intermédiaire |

---

## 🎯 OBJECTIFS PÉDAGOGIQUES

À la fin de cette journée, les participants seront capables de :

1. Expliquer le rôle du Modèle Conceptuel des Traitements (MCT)
2. Identifier les événements et opérations d'un processus métier
3. Construire un MCD selon les règles standard
4. Appliquer les trois premières formes normales
5. Modéliser des relations avancées (ternaires, réflexives)
6. Réaliser un MCD complet pour un système de gestion

---

## 🛠️ MATÉRIEL ET RESSOURCES

### Matériel formateur
- [ ] Vidéoprojecteur
- [ ] Ordinateur avec présentation
- [ ] Tableau blanc et marqueurs
- [ ] Supports de cours imprimés

### Matériel participant
- [ ] Cahier de notes
- [ ] Support de cours Jour 2
- [ ] Fiches d'exercices
- [ ] Travaux du Jour 1

### Documents à distribuer
- [ ] Polycopié "MCT et MCD"
- [ ] Fiche "Règles de normalisation"
- [ ] Exercices Jour 2

---

## ⏰ DÉROULEMENT DÉTAILLÉ

### MATINÉE (9h00 - 12h00)

---

### 🕘 SÉQUENCE 1 : Révision Jour 1 (9h00 - 9h15)

**Durée :** 15 minutes

**Objectif :** Consolider les acquis et clarifier les points restés obscurs

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Rappel des points clés | Exposé | Diaporama |
| 10 min | Questions/Réponses | Participatif | - |

#### Questions de révision
1. Quels sont les niveaux de la méthode Merise ?
2. Comment représente-t-on une entité ?
3. Quelle est la différence entre (0,n) et (1,n) ?
4. Qu'est-ce qu'une relation réflexive ?

---

### 🕘 SÉQUENCE 2 : Modèle MCT (9h15 - 10h15)

**Durée :** 1 heure

**Objectif :** Comprendre le Modèle Conceptuel des Traitements

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 15 min | Événements et synchronisation | Exposé | Diaporama |
| 15 min | Opérations et règles de gestion | Exposé | Diaporama |
| 15 min | Diagramme de flux | Exposé + Démonstration | Diaporama |
| 15 min | Processus métier - Exemples | Exposé + Discussion | Exemples |

#### Contenu détaillé

##### A. Introduction au MCT

**Définition :** Le MCT décrit les traitements du système d'information indépendamment de l'organisation et des moyens.

**Position dans Merise :**
| Niveau | Données | Traitements |
|--------|---------|-------------|
| Conceptuel | MCD | **MCT** |
| Logique | MLD | MLT |
| Physique | MPD | MPT |

##### B. Les Événements

**Définition :** Fait significatif qui déclenche une réaction du système.

**Types d'événements :**
| Type | Description | Exemple |
|------|-------------|---------|
| Événement externe | Vient de l'environnement | Arrivée commande client |
| Événement interne | Produit par le système | Facture émise |
| Événement temporel | Lié au temps | Fin de mois |

**Représentation :**
```
    ┌─────────────────┐
    │ Arrivée         │
    │ commande client │
    └────────┬────────┘
             │
             ▼
```

##### C. La Synchronisation

**Définition :** Condition logique sur les événements pour déclencher une opération.

**Opérateurs :**
- **ET** : Tous les événements doivent être présents
- **OU** : Au moins un événement présent

**Exemple :**
```
┌─────────────┐     ┌─────────────┐
│  Commande   │     │   Stock     │
│  reçue      │     │ disponible  │
└──────┬──────┘     └──────┬──────┘
       │                   │
       └───────┬───────────┘
               │ ET
               ▼
       ┌───────────────┐
       │   VALIDER     │
       │   COMMANDE    │
       └───────────────┘
```

##### D. Les Opérations

**Définition :** Ensemble d'actions exécutées suite à un événement ou une synchronisation.

**Caractéristiques :**
- Non interruptible
- Produit un ou plusieurs résultats
- Soumise à des règles de gestion

**Représentation :**
```
       ┌───────────────────────────┐
       │       OPERATION           │
       ├───────────────────────────┤
       │ - Action 1                │
       │ - Action 2                │
       │ - Action 3                │
       ├───────────────────────────┤
       │ Règles d'émission         │
       └───────────────────────────┘
```

##### E. Règles d'émission

**Définition :** Conditions de production des résultats.

**Exemple complet :**
```
┌─────────────┐
│  Demande    │
│  de prêt    │
└──────┬──────┘
       │
       ▼
┌─────────────────────────────┐
│    ETUDIER DEMANDE          │
├─────────────────────────────┤
│ - Vérifier solvabilité      │
│ - Calculer capacité         │
│ - Analyser risque           │
├─────────────────────────────┤
│ Si solvable : accord        │
│ Si non solvable : refus     │
└─────────────────────────────┘
       │
   ┌───┴───┐
   ▼       ▼
┌─────┐ ┌─────┐
│Accord│ │Refus│
└─────┘ └─────┘
```

##### F. Exercice pratique : Processus de commande

**Contexte :** Modéliser le processus de traitement d'une commande client.

**Éléments :**
- Réception de la commande
- Vérification du stock
- Préparation ou mise en attente
- Expédition

---

### ☕ PAUSE CAFÉ (10h15 - 10h30)

---

### 🕥 SÉQUENCE 3 : Modèle MCD - Partie 1 (10h30 - 12h00)

**Durée :** 1h30

**Objectif :** Maîtriser le formalisme du MCD et les règles de normalisation

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 30 min | Formalisme du MCD | Exposé | Diaporama |
| 30 min | Règles de normalisation | Exposé + Exemples | Diaporama |
| 30 min | Exercices d'identification | Travaux pratiques | Fiche d'exercices |

#### Contenu détaillé

##### A. Formalisme du MCD

**Le MCD représente :**
- Les entités (objets de gestion)
- Les associations (liens entre entités)
- Les propriétés (caractéristiques)
- Les cardinalités (contraintes de participation)

**Notation standard :**
```
┌─────────────────┐          ASSOCIATION          ┌─────────────────┐
│     ENTITE1     │         ┌─────────┐           │     ENTITE2     │
├─────────────────┤  (x,y)  │         │  (x,y)    ├─────────────────┤
│ Identifiant     │─────────│ Libellé │───────────│ Identifiant     │
│ Attribut1       │         │         │           │ Attribut1       │
│ Attribut2       │         │ PropAsso│           │ Attribut2       │
└─────────────────┘         └─────────┘           └─────────────────┘
```

##### B. Les Dépendances Fonctionnelles

**Définition :** Une dépendance fonctionnelle existe quand la connaissance de la valeur d'un attribut permet de déterminer de façon unique la valeur d'un autre attribut.

**Notation :** A → B (A détermine B)

**Exemples :**
- NumEtudiant → Nom, Prénom, DateNaissance
- CodeProduit → Designation, Prix
- (NumCommande, RefProduit) → Quantité

##### C. Règles de Normalisation

###### Première Forme Normale (1FN)

**Règle :** Tous les attributs doivent être atomiques (non décomposables).

**Exemple NON 1FN :**
```
┌─────────────────────────┐
│        CLIENT           │
├─────────────────────────┤
│ NumClient               │
│ Nom                     │
│ Telephones (multiple!)  │  ← NON ATOMIQUE
└─────────────────────────┘
```

**Correction en 1FN :**
```
┌─────────────────┐           ┌─────────────────┐
│     CLIENT      │           │   TELEPHONE     │
├─────────────────┤           ├─────────────────┤
│ NumClient       │───────────│ NumTel          │
│ Nom             │           │ NumClient (FK)  │
└─────────────────┘           │ TypeTel         │
                              └─────────────────┘
```

###### Deuxième Forme Normale (2FN)

**Règle :** Être en 1FN + Tous les attributs non-clés doivent dépendre de la totalité de la clé primaire.

**Exemple NON 2FN :**
```
LIGNE_COMMANDE (NumCommande, RefProduit, Quantité, DesignationProduit)
                 └──────────┬──────────┘     ↑           ↑
                         Clé composée         │           │
                                              │           │
                    Dépend de la clé totale ──┘           │
                    Dépend seulement de RefProduit ───────┘
```

**Correction en 2FN :**
```
LIGNE_COMMANDE (NumCommande, RefProduit, Quantité)
PRODUIT (RefProduit, DesignationProduit)
```

###### Troisième Forme Normale (3FN)

**Règle :** Être en 2FN + Aucun attribut non-clé ne doit dépendre d'un autre attribut non-clé.

**Exemple NON 3FN :**
```
EMPLOYE (NumEmp, Nom, CodeService, NomService)
           ↑                  ↑          ↑
         Clé                  │          │
                              │          │
              Dépend de NumEmp ──────────┘
              Dépend de CodeService ──────┘ (transitive!)
```

**Correction en 3FN :**
```
EMPLOYE (NumEmp, Nom, CodeService)
SERVICE (CodeService, NomService)
```

##### D. Exercice pratique : Normalisation

**Relation à normaliser :**
```
FACTURE (NumFact, DateFact, NumClient, NomClient, AdresseClient, 
         RefProduit, DesignProduit, PrixUnit, Quantite, Montant)
```

**Travail demandé :**
1. Identifier les dépendances fonctionnelles
2. Vérifier chaque forme normale
3. Proposer un schéma normalisé

---

### 🍽️ PAUSE DÉJEUNER (12h00 - 13h30)

---

### APRÈS-MIDI (13h30 - 16h30)

---

### 🕜 SÉQUENCE 4 : Modèle MCD - Partie 2 (13h30 - 15h15)

**Durée :** 1h45

**Objectif :** Maîtriser les concepts avancés du MCD

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 30 min | Entités et relations avancées | Exposé | Diaporama |
| 30 min | Relations ternaires | Exposé + Exercice | Diaporama |
| 30 min | Associations réflexives | Exposé + Exercice | Diaporama |
| 15 min | Cas complexes et exercices | Travaux pratiques | Fiche |

#### Contenu détaillé

##### A. Relations Ternaires

**Définition :** Association impliquant trois entités.

**Quand utiliser :** Lorsque la relation entre deux entités dépend d'une troisième.

**Exemple : Affectation COURS-PROFESSEUR-SALLE**
```
                    ┌───────────────┐
                    │     SALLE     │
                    ├───────────────┤
                    │ NumSalle      │
                    │ Capacite      │
                    └───────┬───────┘
                            │ (0,n)
                            │
                    ┌───────┴───────┐
                    │   AFFECTER    │
                    │               │
                    │   Horaire     │
                    │   Jour        │
                    └───────────────┘
                   ╱                 ╲
            (1,n) ╱                   ╲ (1,n)
                 ╱                     ╲
┌───────────────┐                       ┌───────────────┐
│     COURS     │                       │  PROFESSEUR   │
├───────────────┤                       ├───────────────┤
│ CodeCours     │                       │ NumProf       │
│ Intitule      │                       │ Nom           │
└───────────────┘                       └───────────────┘
```

**Lecture :** Un cours est dispensé par un professeur dans une salle à un horaire donné.

##### B. Associations Réflexives

**Définition :** Association d'une entité avec elle-même.

**Types courants :**

###### 1. Hiérarchie (supervision)
```
                    ┌──────────────────────┐
                    │                      │
         (0,n)      ▼                      │ (0,1)
        Subordonnés                        │ Supérieur
                    │                      │
              ┌─────┴─────┐                │
              │  EMPLOYE  │────────────────┘
              ├───────────┤    SUPERVISE
              │ NumEmp    │
              │ Nom       │
              └───────────┘
```

###### 2. Nomenclature (composition)
```
                    ┌──────────────────────┐
                    │                      │
         (0,n)      ▼                      │ (0,n)
        Composants                         │ Composés
                    │                      │
              ┌─────┴─────┐                │
              │  PRODUIT  │────────────────┘
              ├───────────┤   SE_COMPOSE
              │ RefProd   │       │
              │ Design    │   Quantite
              └───────────┘
```

###### 3. Parrainage
```
                    ┌──────────────────────┐
                    │                      │
         (0,n)      ▼                      │ (0,1)
        Filleuls                           │ Parrain
                    │                      │
              ┌─────┴─────┐                │
              │  CLIENT   │────────────────┘
              ├───────────┤   PARRAINER
              │ NumClient │
              │ Nom       │
              └───────────┘
```

##### C. Exercice pratique : Organigramme d'entreprise

**Contexte :**
Une entreprise veut modéliser son organigramme. Chaque employé a un supérieur hiérarchique (sauf le directeur). Un employé peut encadrer plusieurs subordonnés.

**Travail demandé :**
Réaliser le MCD avec l'association réflexive.

##### D. Héritage et Spécialisation

**Concept :** Une entité générique peut être spécialisée en sous-types.

**Exemple : Personnes dans un établissement**
```
                    ┌───────────────┐
                    │   PERSONNE    │
                    ├───────────────┤
                    │ NumPers       │
                    │ Nom           │
                    │ Prenom        │
                    └───────┬───────┘
                            │
              ┌─────────────┼─────────────┐
              │             │             │
              ▼             ▼             ▼
       ┌───────────┐ ┌───────────┐ ┌───────────┐
       │  ETUDIANT │ │ PROFESSEUR│ │  ADMIN    │
       ├───────────┤ ├───────────┤ ├───────────┤
       │ NumEtu    │ │ Grade     │ │ Fonction  │
       │ Filiere   │ │ Specialite│ │ Service   │
       └───────────┘ └───────────┘ └───────────┘
```

---

### ☕ PAUSE (15h15 - 15h30)

---

### 🕞 SÉQUENCE 5 : Modèle MCD - Partie 3 (15h30 - 16h30)

**Durée :** 1 heure

**Objectif :** Réaliser un MCD complet

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 45 min | Étude de cas : Gestion commerciale | Travail en groupe | Énoncé |
| 10 min | Présentation des travaux | Exposé participatif | Tableau |
| 5 min | Synthèse du jour | Exposé | - |

---

#### 📝 ÉTUDE DE CAS : Système de Gestion Commerciale

**Contexte :**
Une entreprise de vente de matériel informatique souhaite informatiser sa gestion commerciale.

**Description du système :**

1. **Clients**
   - Numéro client, nom, adresse, téléphone, email
   - Un client peut être une entreprise ou un particulier
   - Les entreprises ont un numéro SIRET

2. **Produits**
   - Référence, désignation, prix unitaire HT, quantité en stock
   - Chaque produit appartient à une catégorie
   - Un produit peut être composé d'autres produits (pack)

3. **Commandes**
   - Numéro commande, date commande, statut
   - Une commande est passée par un seul client
   - Une commande contient plusieurs lignes (produit + quantité)

4. **Fournisseurs**
   - Code fournisseur, raison sociale, adresse, téléphone
   - Un fournisseur peut fournir plusieurs produits
   - Un produit peut être fourni par plusieurs fournisseurs

5. **Catégories**
   - Code catégorie, libellé, description
   - Une catégorie peut contenir des sous-catégories

**Travail demandé :**
1. Identifier toutes les entités
2. Définir les attributs de chaque entité
3. Identifier les associations et leurs cardinalités
4. Dessiner le MCD complet

**Solution attendue (schéma simplifié) :**
```
┌─────────────┐                               ┌─────────────┐
│  CATEGORIE  │◄──────────────────────────────│  CATEGORIE  │
├─────────────┤        SOUS_CAT               ├─────────────┤
│ CodeCat     │                               │ (réflexive) │
│ Libelle     │                               └─────────────┘
└──────┬──────┘
       │ (1,1)
       │
       │ (0,n)
┌──────┴──────┐         (0,n)        (1,n)   ┌─────────────┐
│   PRODUIT   │◄─────────────FOURNIR─────────│ FOURNISSEUR │
├─────────────┤              │               ├─────────────┤
│ RefProd     │          PrixAchat           │ CodeFourn   │
│ Designation │          Delai               │ RaisonSoc   │
│ PrixUnitHT  │                              │ Adresse     │
│ QteStock    │                              │ Tel         │
└──────┬──────┘                              └─────────────┘
       │
       │ (0,n)
       │
┌──────┴──────┐
│  CONTENIR   │◄─── Quantite, PrixVente
└──────┬──────┘
       │ (1,n)
       │
┌──────┴──────┐         (1,n)        (1,1)   ┌─────────────┐
│  COMMANDE   │◄─────────────PASSER──────────│   CLIENT    │
├─────────────┤                              ├─────────────┤
│ NumCmd      │                              │ NumClient   │
│ DateCmd     │                              │ Nom         │
│ Statut      │                              │ Adresse     │
└─────────────┘                              │ Tel         │
                                             │ Email       │
                                             └─────────────┘
```

---

## ✅ SYNTHÈSE DU JOUR 2

### Points clés à retenir

| Concept | Définition |
|---------|------------|
| **MCT** | Modèle des traitements indépendant de l'organisation |
| **Événement** | Fait significatif déclenchant une réaction |
| **Opération** | Ensemble d'actions non interruptibles |
| **1FN** | Attributs atomiques |
| **2FN** | Dépendance totale de la clé |
| **3FN** | Pas de dépendance transitive |
| **Relation ternaire** | Association entre 3 entités |
| **Relation réflexive** | Entité en relation avec elle-même |

### Préparation Jour 3
- Revoir les règles de transformation MCD → MLD
- Apporter les exercices corrigés

---

## 📊 ÉVALUATION DE LA SÉANCE

### Grille d'observation formateur

| Critère | Non acquis | En cours | Acquis |
|---------|------------|----------|--------|
| Compréhension du MCT | ☐ | ☐ | ☐ |
| Maîtrise des formes normales | ☐ | ☐ | ☐ |
| Construction d'un MCD | ☐ | ☐ | ☐ |
| Relations ternaires | ☐ | ☐ | ☐ |
| Relations réflexives | ☐ | ☐ | ☐ |

### Auto-évaluation participant

1. Je comprends le rôle du MCT : ☐ Oui ☐ Partiellement ☐ Non
2. Je maîtrise les 3 formes normales : ☐ Oui ☐ Partiellement ☐ Non
3. Je sais créer un MCD complet : ☐ Oui ☐ Partiellement ☐ Non

---

## 📎 DOCUMENTS ANNEXES JOUR 2

- Annexe 2A : Diaporama "MCT et MCD"
- Annexe 2B : Fiche "Règles de normalisation"
- Annexe 2C : Exercices et corrigés Jour 2
- Annexe 2D : Étude de cas détaillée
