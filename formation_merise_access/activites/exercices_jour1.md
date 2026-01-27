# Exercices Jour 1 - Introduction à Merise et Modélisation E/A

## Exercice 1 : Identification d'Entités et Attributs

### Énoncé
Pour chacun des contextes suivants, identifiez les entités et leurs attributs.

### Contexte 1 : Agence de Voyage
Une agence de voyage gère des voyages, des clients et des réservations.

**Travail demandé** :
1. Identifiez les entités
2. Listez les attributs de chaque entité
3. Définissez l'identifiant de chaque entité

### Contexte 2 : Cabinet Médical
Un cabinet médical gère les médecins, les patients et les consultations.

**Travail demandé** :
1. Identifiez les entités
2. Listez les attributs de chaque entité
3. Définissez l'identifiant de chaque entité

### Contexte 3 : Location de Véhicules
Une entreprise de location gère un parc de véhicules, des clients et des contrats de location.

**Travail demandé** :
1. Identifiez les entités
2. Listez les attributs de chaque entité
3. Définissez l'identifiant de chaque entité

---

## Exercice 2 : Détermination des Cardinalités

### Énoncé
Pour chaque situation, déterminez les cardinalités appropriées.

### Situation 1
Un EMPLOYE appartient à un et un seul DEPARTEMENT.
Un DEPARTEMENT peut avoir plusieurs EMPLOYES.

**Cardinalités** : EMPLOYE (___,___) appartient (___,___) DEPARTEMENT

### Situation 2
Un CLIENT peut passer plusieurs COMMANDES ou aucune.
Une COMMANDE est passée par un et un seul CLIENT.

**Cardinalités** : CLIENT (___,___) passe (___,___) COMMANDE

### Situation 3
Un ETUDIANT peut s'inscrire à plusieurs COURS.
Un COURS peut avoir plusieurs ETUDIANTS inscrits.

**Cardinalités** : ETUDIANT (___,___) inscrit (___,___) COURS

### Situation 4
Un LIVRE peut être écrit par plusieurs AUTEURS.
Un AUTEUR peut écrire plusieurs LIVRES.

**Cardinalités** : LIVRE (___,___) écrit (___,___) AUTEUR

### Situation 5
Un EMPLOYE peut avoir un seul BUREAU.
Un BUREAU peut être attribué à un seul EMPLOYE ou être vacant.

**Cardinalités** : EMPLOYE (___,___) occupe (___,___) BUREAU

---

## Exercice 3 : Lecture d'un Modèle E/A

### Énoncé
Analysez le modèle E/A suivant et répondez aux questions.

```
┌─────────────────┐  1,1        0,n  ┌─────────────────┐
│    VEHICULE     │──────────────────│   CATEGORIE     │
├─────────────────┤   appartient     ├─────────────────┤
│ Immatriculation │                  │ CodeCategorie   │
│ Marque          │                  │ LibelleCategorie│
│ Modele          │                  │ TarifJournalier │
│ Annee           │                  └─────────────────┘
│ Kilometrage     │
└────────┬────────┘
         │
    0,n  │ fait l'objet
         │ DateDebut
         │ DateFin
         │ KmDebut
         │ KmFin
         │
┌────────┴────────┐  1,1        0,n  ┌─────────────────┐
│    LOCATION     │──────────────────│     CLIENT      │
├─────────────────┤   effectue       ├─────────────────┤
│ NumLocation     │                  │ NumClient       │
│ MontantTotal    │                  │ NomClient       │
│ Statut          │                  │ PrenomClient    │
└─────────────────┘                  │ PermisNumero    │
                                     │ Telephone       │
                                     └─────────────────┘
```

### Questions

1. Combien de catégories un véhicule peut-il avoir ?
2. Un client peut-il effectuer plusieurs locations ?
3. Un véhicule peut-il faire l'objet de plusieurs locations ?
4. Quels attributs caractérisent la relation "fait l'objet" ?
5. Quel est l'identifiant de l'entité VEHICULE ?

---

## Exercice 4 : Modélisation Complète

### Énoncé
Un club de sport souhaite gérer :
- Ses **adhérents** (numéro, nom, prénom, date de naissance, adresse, téléphone, date d'adhésion)
- Les **activités** proposées (code, nom, description, niveau requis)
- Les **coachs** (numéro, nom, prénom, spécialité, téléphone)
- Les **séances** d'entraînement (date, heure, durée, salle)

### Règles de Gestion
1. Un adhérent peut s'inscrire à plusieurs activités
2. Une activité peut avoir plusieurs adhérents
3. Un coach peut encadrer plusieurs activités
4. Une activité n'a qu'un seul coach principal
5. Une séance concerne une seule activité
6. Une activité peut avoir plusieurs séances

### Travail Demandé
1. Dessinez le modèle E/A complet
2. Précisez toutes les cardinalités
3. Identifiez les attributs de chaque relation (s'il y en a)

---

## Exercice 5 : Correction d'Erreurs

### Énoncé
Le modèle E/A suivant contient des erreurs. Identifiez-les et proposez des corrections.

```
┌─────────────────┐  0,n        1,n  ┌─────────────────┐
│    PRODUIT      │──────────────────│   FOURNISSEUR   │
├─────────────────┤   fournit        ├─────────────────┤
│ RefProduit      │                  │ CodeFournisseur │
│ Designation     │                  │ RaisonSociale   │
│ Prix            │                  │ Adresse         │
│ NomFournisseur  │                  │ Email           │
│ Stock           │                  │ Produits        │
└─────────────────┘                  └─────────────────┘
```

### Questions
1. Quelles erreurs identifiez-vous dans ce modèle ?
2. Proposez un modèle corrigé

---

## Exercice 6 : Cas Pratique - Restaurant

### Contexte
Un restaurant souhaite informatiser sa gestion. Il a besoin de gérer :
- Les plats proposés (avec ingrédients et prix)
- Les clients et leurs réservations de tables
- Les commandes passées par les clients
- Les tables du restaurant

### Travail Demandé
1. Listez les entités nécessaires
2. Définissez les attributs de chaque entité
3. Identifiez les relations et leurs cardinalités
4. Dessinez le modèle E/A complet

---

## Exercice 7 : Questions de Réflexion

### Question 1
Pourquoi est-il important de définir un identifiant pour chaque entité ?

### Question 2
Dans quels cas une relation peut-elle avoir des attributs propres ?

### Question 3
Quelle est la différence entre une cardinalité (0,n) et (1,n) ?

### Question 4
Comment modéliser le fait qu'un employé peut avoir un supérieur hiérarchique ?

---

## Exercice Bonus : Analyse de Situation

### Énoncé
Un enseignant vous présente le système suivant :
"Dans mon établissement, chaque élève est inscrit dans une classe. Chaque classe a un professeur principal. Les professeurs enseignent plusieurs matières. Les élèves ont des notes dans chaque matière."

### Travail Demandé
1. Identifiez toutes les entités
2. Proposez un modèle E/A qui représente cette situation
3. Discutez des choix de modélisation
