# FICHE DE DÉROULEMENT - JOUR 1
## Introduction à Merise et Modélisation Entité/Association

---

## 📋 INFORMATIONS DE LA SÉANCE

| Élément | Description |
|---------|-------------|
| **Jour** | Jour 1 sur 5 |
| **Durée** | 6 heures |
| **Thème** | Introduction à Merise et Modélisation E/A |
| **Public** | Professeurs d'Économie et Gestion |
| **Niveau** | Intermédiaire |

---

## 🎯 OBJECTIFS PÉDAGOGIQUES

À la fin de cette journée, les participants seront capables de :

1. Expliquer les principes fondamentaux de la méthode Merise
2. Définir ce qu'est un SGBD et son rôle
3. Identifier les entités dans un contexte donné
4. Définir les attributs et propriétés des entités
5. Créer des relations avec les cardinalités appropriées
6. Réaliser un modèle E/A simple

---

## 🛠️ MATÉRIEL ET RESSOURCES

### Matériel formateur
- [ ] Vidéoprojecteur
- [ ] Ordinateur avec présentation PowerPoint
- [ ] Tableau blanc et marqueurs
- [ ] Supports de cours imprimés

### Matériel participant
- [ ] Cahier de notes
- [ ] Support de cours Jour 1
- [ ] Fiches d'exercices

### Documents à distribuer
- [ ] Polycopié "Introduction à Merise"
- [ ] Fiche récapitulative "Modèle E/A"
- [ ] Exercices Jour 1

---

## ⏰ DÉROULEMENT DÉTAILLÉ

### MATINÉE (9h00 - 12h00)

---

### 🕘 SÉQUENCE 1 : Accueil et Introduction (9h00 - 9h15)

**Durée :** 15 minutes

**Objectif :** Créer une dynamique de groupe et présenter la formation

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Tour de table des participants | Participatif | - |
| 5 min | Présentation du formateur | Exposé | - |
| 5 min | Présentation du programme | Exposé | Diaporama |

#### Consignes pour le formateur
1. Accueillir chaleureusement les participants
2. Demander à chaque participant de se présenter (nom, établissement, attentes)
3. Présenter les objectifs de la formation
4. Distribuer le programme détaillé
5. Expliquer les modalités pratiques (pauses, repas, questions)

#### Points clés à aborder
- ✅ Objectifs de la formation sur 5 jours
- ✅ Déroulement type d'une journée
- ✅ Modalités d'évaluation
- ✅ Ressources disponibles

---

### 🕘 SÉQUENCE 2 : Présentation générale et Notion SGBD (9h15 - 10h15)

**Durée :** 1 heure

**Objectif :** Comprendre les fondements de Merise et des SGBD

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 15 min | Introduction à Merise | Exposé | Diaporama |
| 15 min | Histoire et contexte | Exposé | Diaporama |
| 15 min | Systèmes de Gestion de Bases de Données | Exposé + Démonstration | Diaporama + Logiciel |
| 15 min | Importance dans l'enseignement | Discussion | Tableau blanc |

#### Contenu détaillé

##### A. Introduction à la méthode Merise
- **Définition** : Méthode d'analyse et de conception des systèmes d'information
- **Signification** : Méthode d'Étude et de Réalisation Informatique pour les Systèmes d'Entreprise
- **Principes fondamentaux** :
  - Séparation données/traitements
  - Approche par niveaux d'abstraction
  - Cycle de vie du projet

##### B. Histoire et contexte
- Création : France, 1978-1979
- Contexte : Besoin de méthodes structurées
- Évolution : Merise/2, extensions

##### C. Niveaux de Merise
| Niveau | Données | Traitements |
|--------|---------|-------------|
| Conceptuel | MCD | MCT |
| Logique | MLD | MLT |
| Physique | MPD | MPT |

##### D. Systèmes de Gestion de Bases de Données
- **Définition** : Logiciel pour créer et gérer des bases de données
- **Types** :
  - Hiérarchique (années 60)
  - Réseau (années 70)
  - Relationnel (années 80) ⭐
  - Objet (années 90)
- **Exemples** : Access, MySQL, Oracle, SQL Server

##### E. Importance pédagogique
- Applications dans l'enseignement économie-gestion
- Compétences transférables aux élèves
- Préparation aux examens (BTS, DCG...)

#### Questions de vérification
1. Que signifie l'acronyme MERISE ?
2. Quels sont les 3 niveaux de Merise ?
3. Qu'est-ce qu'un SGBD ?
4. Quel type de SGBD utilisons-nous principalement aujourd'hui ?

---

### ☕ PAUSE CAFÉ (10h15 - 10h30)

---

### 🕥 SÉQUENCE 3 : Modèle E/A - Partie 1 (10h30 - 12h00)

**Durée :** 1h30

**Objectif :** Maîtriser les concepts d'entités et d'attributs

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 30 min | Concepts fondamentaux : entités | Exposé | Diaporama |
| 30 min | Attributs et propriétés | Exposé + Exercice | Diaporama + Fiche |
| 30 min | Exemples et exercices | Travaux pratiques | Fiche d'exercices |

#### Contenu détaillé

##### A. Les Entités

**Définition :** Une entité représente un objet du monde réel ayant une existence propre.

**Caractéristiques :**
- Nom unique et significatif (substantif au singulier)
- Au moins un attribut identifiant
- Représentée par un rectangle

**Exemples :**
```
┌─────────────┐
│   CLIENT    │
├─────────────┤
│ NumClient   │ ← Identifiant (souligné)
│ Nom         │
│ Prénom      │
│ Adresse     │
│ Téléphone   │
└─────────────┘
```

##### B. Les Attributs

**Définition :** Caractéristique ou propriété d'une entité.

**Types d'attributs :**
| Type | Description | Exemple |
|------|-------------|---------|
| Identifiant | Unique, identifie l'entité | NumClient |
| Simple | Valeur atomique | Nom |
| Composé | Plusieurs parties | Adresse (rue, ville, CP) |
| Dérivé | Calculé à partir d'autres | Âge (depuis date naissance) |
| Multivalué | Plusieurs valeurs | Téléphones |

**Règles de nommage :**
- Nom significatif
- Éviter les espaces et accents
- Préfixer avec le nom de l'entité si nécessaire

##### C. Exercice pratique 1 : Identification d'entités

**Contexte :** Une librairie souhaite gérer ses livres et ses clients.

**Consigne :** Identifiez les entités et leurs attributs.

**Éléments fournis :**
- La librairie vend des livres
- Chaque livre a un ISBN, un titre, un auteur, un prix
- Les clients ont un numéro, nom, prénom, email
- Les clients achètent des livres

**Solution attendue :**

```
┌─────────────┐          ┌─────────────┐
│    LIVRE    │          │   CLIENT    │
├─────────────┤          ├─────────────┤
│ ISBN        │          │ NumClient   │
│ Titre       │          │ Nom         │
│ Auteur      │          │ Prénom      │
│ Prix        │          │ Email       │
└─────────────┘          └─────────────┘
```

#### Questions de vérification
1. Qu'est-ce qu'une entité ?
2. Quel est le rôle d'un identifiant ?
3. Citez 3 types d'attributs différents.

---

### 🍽️ PAUSE DÉJEUNER (12h00 - 13h30)

---

### APRÈS-MIDI (13h30 - 16h30)

---

### 🕜 SÉQUENCE 4 : Modèle E/A - Partie 2 (13h30 - 15h15)

**Durée :** 1h45

**Objectif :** Maîtriser les relations et cardinalités

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 30 min | Relations et associations | Exposé | Diaporama |
| 30 min | Cardinalités et contraintes | Exposé + Démonstration | Diaporama |
| 30 min | Types de relations | Exposé | Diaporama |
| 15 min | Exercices guidés | Travaux pratiques | Fiche d'exercices |

#### Contenu détaillé

##### A. Les Relations (Associations)

**Définition :** Lien sémantique entre deux ou plusieurs entités.

**Représentation :**
```
┌─────────┐         ┌─────────┐         ┌─────────┐
│ CLIENT  │─────────│ ACHETER │─────────│  LIVRE  │
└─────────┘         └─────────┘         └─────────┘
```

**Nommage :**
- Verbe à l'infinitif (ACHETER, APPARTENIR, CONCERNER)
- Nom d'action (ACHAT, INSCRIPTION)

##### B. Les Cardinalités

**Définition :** Nombre minimum et maximum d'occurrences d'une entité dans une relation.

**Notation :** (min, max)

| Cardinalité | Signification |
|-------------|---------------|
| (0,1) | Optionnel, au plus 1 |
| (1,1) | Obligatoire, exactement 1 |
| (0,n) | Optionnel, plusieurs possibles |
| (1,n) | Obligatoire, au moins 1 |

**Méthode de lecture :**
> "Un CLIENT peut acheter de 0 à n LIVRE(s)"
> "Un LIVRE peut être acheté par de 0 à n CLIENT(s)"

**Exemple complet :**
```
┌─────────┐  (0,n)      (1,n) ┌─────────┐
│ CLIENT  │───────ACHETER─────│  LIVRE  │
└─────────┘       │           └─────────┘
                  │
            DateAchat
            Quantité
```

##### C. Types de relations

| Type | Description | Exemple |
|------|-------------|---------|
| Binaire | Entre 2 entités | CLIENT-COMMANDE |
| Ternaire | Entre 3 entités | ETUDIANT-COURS-SALLE |
| Réflexive | Une entité avec elle-même | EMPLOYE (supervise) |

**Relation réflexive :**
```
        ┌───────────────┐
        │               │
        ▼   (0,n)       │(0,1)
┌───────────────┐       │
│    EMPLOYE    │───────┘
│               │  SUPERVISE
└───────────────┘
```

##### D. Exercice pratique 2 : Création de relations

**Contexte :** Système de gestion scolaire

**Éléments :**
- Un professeur enseigne plusieurs matières
- Une matière est enseignée par un seul professeur
- Un élève suit plusieurs matières
- Une matière est suivie par plusieurs élèves

**Consigne :** Dessiner le modèle E/A avec les cardinalités.

**Solution attendue :**
```
┌───────────┐ (1,n)    (1,1) ┌───────────┐ (0,n)    (1,n) ┌───────────┐
│ PROFESSEUR│────ENSEIGNER───│  MATIERE  │────SUIVRE──────│   ELEVE   │
└───────────┘                └───────────┘                └───────────┘
```

---

### ☕ PAUSE (15h15 - 15h30)

---

### 🕞 SÉQUENCE 5 : Modèle E/A - Partie 3 (15h30 - 16h30)

**Durée :** 1 heure

**Objectif :** Appliquer les concepts à des cas concrets

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 20 min | Étude de cas 1 : Gestion étudiants | Travail en groupe | Énoncé de cas |
| 20 min | Étude de cas 2 : Gestion de stock | Travail en groupe | Énoncé de cas |
| 15 min | Correction collective | Exposé participatif | Tableau blanc |
| 5 min | Synthèse du jour | Exposé | - |

---

#### 📝 ÉTUDE DE CAS 1 : Gestion des Étudiants

**Contexte :**
Une université souhaite mettre en place un système de gestion des inscriptions aux cours.

**Règles de gestion :**
1. Un étudiant est identifié par son numéro d'étudiant
2. Un étudiant possède un nom, prénom, date de naissance, adresse email
3. Un cours est identifié par un code et possède un intitulé et un nombre de crédits
4. Un étudiant peut s'inscrire à plusieurs cours
5. Un cours peut accueillir plusieurs étudiants
6. Pour chaque inscription, on retient la date d'inscription

**Travail demandé :**
1. Identifier les entités et leurs attributs
2. Identifier les relations
3. Déterminer les cardinalités
4. Dessiner le modèle E/A complet

**Solution :**
```
┌─────────────────┐                          ┌─────────────────┐
│    ETUDIANT     │                          │      COURS      │
├─────────────────┤                          ├─────────────────┤
│ NumEtudiant     │  (0,n)         (0,n)     │ CodeCours       │
│ Nom             │─────── INSCRIPTION ──────│ Intitule        │
│ Prenom          │           │              │ NbCredits       │
│ DateNaissance   │      DateInscription     └─────────────────┘
│ Email           │                          
└─────────────────┘                          
```

---

#### 📝 ÉTUDE DE CAS 2 : Gestion de Stock

**Contexte :**
Une entreprise commerciale veut gérer ses produits et fournisseurs.

**Règles de gestion :**
1. Un produit est identifié par une référence
2. Un produit a une désignation, un prix unitaire, une quantité en stock
3. Un fournisseur est identifié par un code
4. Un fournisseur a une raison sociale, adresse, téléphone
5. Un produit peut être fourni par plusieurs fournisseurs
6. Un fournisseur peut fournir plusieurs produits
7. Pour chaque approvisionnement, on note le prix d'achat et le délai de livraison

**Travail demandé :**
Réaliser le modèle E/A complet.

**Solution :**
```
┌─────────────────┐                          ┌─────────────────┐
│    PRODUIT      │                          │  FOURNISSEUR    │
├─────────────────┤                          ├─────────────────┤
│ RefProduit      │  (1,n)         (1,n)     │ CodeFourn       │
│ Designation     │───── APPROVISIONNER ─────│ RaisonSociale   │
│ PrixUnitaire    │           │              │ Adresse         │
│ QteStock        │      PrixAchat           │ Telephone       │
└─────────────────┘      DelaiLivraison      └─────────────────┘
```

---

## ✅ SYNTHÈSE DU JOUR 1

### Points clés à retenir

| Concept | Définition |
|---------|------------|
| **Merise** | Méthode de conception de SI (séparation données/traitements) |
| **SGBD** | Logiciel pour créer et gérer des bases de données |
| **Entité** | Objet du monde réel avec existence propre |
| **Attribut** | Caractéristique d'une entité |
| **Identifiant** | Attribut unique identifiant une occurrence |
| **Relation** | Lien sémantique entre entités |
| **Cardinalité** | Nombre min/max d'occurrences dans une relation |

### Exercice à préparer pour le Jour 2
Réfléchir à un cas de gestion lié à votre établissement (CDI, notes, absences...) et identifier les entités potentielles.

---

## 📊 ÉVALUATION DE LA SÉANCE

### Grille d'observation formateur

| Critère | Non acquis | En cours | Acquis |
|---------|------------|----------|--------|
| Compréhension de Merise | ☐ | ☐ | ☐ |
| Identification d'entités | ☐ | ☐ | ☐ |
| Définition d'attributs | ☐ | ☐ | ☐ |
| Création de relations | ☐ | ☐ | ☐ |
| Détermination des cardinalités | ☐ | ☐ | ☐ |

### Questions d'auto-évaluation (participant)

1. Je peux expliquer ce qu'est la méthode Merise : ☐ Oui ☐ Non
2. Je sais identifier les entités dans un énoncé : ☐ Oui ☐ Non
3. Je maîtrise la notion de cardinalité : ☐ Oui ☐ Non
4. Je peux créer un modèle E/A simple : ☐ Oui ☐ Non

---

## 📎 DOCUMENTS ANNEXES JOUR 1

- Annexe 1A : Diaporama "Introduction à Merise"
- Annexe 1B : Fiche récapitulative "Modèle E/A"
- Annexe 1C : Exercices et corrigés Jour 1
- Annexe 1D : Bibliographie et ressources
