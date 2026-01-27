# Corrigés Jour 2 - MCT et MCD

## Exercice 1 : Modèle Conceptuel des Traitements (MCT)

### Processus 1 : Demande de Congés

```
    ╭────────────────────────╮
    │ Demande congés reçue   │
    ╰───────────┬────────────╯
                │
                ↓
┌────────────────────────────────────────┐
│      VERIFIER JOURS DISPONIBLES        │
├────────────────────────────────────────┤
│  - Consulter le solde de congés        │
│  - Comparer avec les jours demandés    │
├────────────────────────────────────────┤
│  Jours suffisants → Jours OK           │
│  Jours insuffisants → Jours NOK        │
└────────────────────────────────────────┘
          /                 \
    ╭────┴────╮         ╭────┴────╮
    │ Jours OK│         │Jours NOK│
    ╰────┬────╯         ╰────┬────╯
         │                   │
         ↓                   ↓
┌────────────────────┐  ┌────────────────────┐
│ VALIDER DEMANDE    │  │ REJETER DEMANDE    │
├────────────────────┤  ├────────────────────┤
│ - Créer absence    │  │ - Notifier refus   │
│ - Décrémenter solde│  │ - Expliquer raison │
├────────────────────┤  ├────────────────────┤
│ Toujours → Acceptée│  │ Toujours → Refusée │
└────────────────────┘  └────────────────────┘
         │                   │
    ╭────┴────╮         ╭────┴────╮
    │ Demande │         │ Demande │
    │ acceptée│         │ refusée │
    ╰─────────╯         ╰─────────╯
```

### Processus 2 : Traitement Réclamation

```
    ╭───────────────────────╮
    │ Réclamation déposée   │
    ╰───────────┬───────────╯
                │
                ↓
┌────────────────────────────────────────┐
│        EXAMINER RECLAMATION            │
├────────────────────────────────────────┤
│  - Analyser le motif                   │
│  - Vérifier les justificatifs          │
│  - Consulter l'historique client       │
├────────────────────────────────────────┤
│  Réclamation fondée → Fondée           │
│  Réclamation non fondée → Non fondée   │
└────────────────────────────────────────┘
          /                 \
    ╭────┴────╮         ╭────┴──────╮
    │ Fondée  │         │Non fondée │
    ╰────┬────╯         ╰────┬──────╯
         │                   │
         ↓                   ↓
┌────────────────────┐  ┌────────────────────┐
│ PROPOSER           │  │ REJETER AVEC       │
│ DEDOMMAGEMENT      │  │ EXPLICATION        │
├────────────────────┤  ├────────────────────┤
│ - Calculer montant │  │ - Rédiger réponse  │
│ - Créer avoir      │  │ - Expliquer motifs │
├────────────────────┤  ├────────────────────┤
│ Toujours → Proposé │  │ Toujours → Rejetée │
└────────────────────┘  └────────────────────┘
         │                   │
    ╭────┴───────╮      ╭────┴──────╮
    │Dédommagement    │ │Réclamation│
    │ proposé    │      │ rejetée   │
    ╰────────────╯      ╰───────────╯
```

### Processus 3 : Inscription à un Examen

```
    ╭─────────────────╮     ╭─────────────────╮
    │ Demande inscr.  │     │ Paiement reçu   │
    ╰────────┬────────╯     ╰────────┬────────╯
             │        ET            │
             └──────────┬───────────┘
                        ↓
┌────────────────────────────────────────┐
│         VERIFIER PREREQUISITES          │
├────────────────────────────────────────┤
│  - Consulter le dossier étudiant       │
│  - Vérifier les prérequis du cours     │
│  - Vérifier le paiement                │
├────────────────────────────────────────┤
│  Prérequis OK ET Payé → Validé         │
│  Prérequis NOK → Refusé                │
│  Non payé → Attente paiement           │
└────────────────────────────────────────┘
      /           |           \
╭────┴────╮  ╭────┴────╮  ╭────┴───────╮
│ Validé  │  │ Refusé  │  │  Attente   │
│         │  │         │  │ paiement   │
╰────┬────╯  ╰────┬────╯  ╰────────────╯
     │            │
     ↓            ↓
┌────────────┐ ┌────────────┐
│ CONFIRMER  │ │ NOTIFIER   │
│ INSCRIPTION│ │ REFUS      │
└────────────┘ └────────────┘
```

---

## Exercice 2 : Normalisation 1FN

### Table 1 : EMPLOYE (Corrigée)

**Tables normalisées** :
```
EMPLOYE (NumEmploye, Nom)
         └─ PK ──┘

TELEPHONE_EMPLOYE (#NumEmploye, Telephone)
                   └───── PK ──────────┘

COMPETENCE_EMPLOYE (#NumEmploye, Competence)
                    └───── PK ──────────┘
```

### Table 2 : COMMANDE (Corrigée)

**Tables normalisées** :
```
COMMANDE (NumCommande, Client)
          └─ PK ────┘

LIGNE_COMMANDE (#NumCommande, #RefProduit, Quantite)
                └────────── PK ─────────┘
```

### Table 3 : COURS (Corrigée)

**Tables normalisées** :
```
COURS (CodeCours, Intitule)
       └─ PK ──┘

ENSEIGNANT_COURS (#CodeCours, #NumEnseignant)
                  └────── PK ─────────────┘

HORAIRE_COURS (#CodeCours, Jour, Heure)
               └────── PK ─────────┘
```

---

## Exercice 3 : Normalisation 2FN et 3FN

### Table 1 : INSCRIPTION (2FN)

**Clé primaire** : (NumEtudiant, CodeCours)

**Problème 2FN** :
- NomEtudiant dépend uniquement de NumEtudiant (pas de toute la clé)
- IntituleCours dépend uniquement de CodeCours (pas de toute la clé)

**Correction** :
```
ETUDIANT (NumEtudiant, NomEtudiant)
          └─ PK ────┘

COURS (CodeCours, IntituleCours)
       └─ PK ──┘

INSCRIPTION (#NumEtudiant, #CodeCours, Note)
             └────────── PK ─────────┘
```

### Table 2 : EMPLOYE (3FN)

**Dépendance transitive** :
- NumEmploye → CodeService
- CodeService → NomService, LocalisationService

Donc : NumEmploye → NomService (via CodeService) = dépendance transitive

**Correction** :
```
SERVICE (CodeService, NomService, LocalisationService)
         └─ PK ───┘

EMPLOYE (NumEmploye, Nom, #CodeService)
         └─ PK ───┘      └─── FK ───┘
```

---

## Exercice 4 : Dépendances Fonctionnelles

### Contexte 1 : Facture

```
NumFacture → DateFacture, MontantTotal
NumFacture → NumClient
NumClient → NomClient, AdresseClient

DF complètes :
- NumFacture → DateFacture
- NumFacture → NumClient
- NumFacture → MontantTotal
- NumClient → NomClient
- NumClient → AdresseClient
```

### Contexte 2 : Ligne de Commande

```
(NumCommande, RefProduit) → Quantite, MontantLigne
RefProduit → Designation, PrixUnitaire

DF complètes :
- (NumCommande, RefProduit) → Quantite
- (NumCommande, RefProduit) → MontantLigne (dérivé: Quantite * PrixUnitaire)
- RefProduit → Designation
- RefProduit → PrixUnitaire
```

### Contexte 3 : Étudiant

```
NumEtudiant → Nom, Prenom, DateNaissance
NumEtudiant → CodeClasse
CodeClasse → NomClasse
CodeClasse → NomProfPrincipal (via une autre entité)

DF avec dépendance transitive :
- NumEtudiant → NomClasse (via CodeClasse)
```

---

## Exercice 5 : MCD Gestion de Projet

```
┌─────────────────┐                           ┌─────────────────┐
│     CLIENT      │                           │     PROJET      │
├─────────────────┤                           ├─────────────────┤
│ CodeClient (PK) │◄──────────────────────────│ CodeProjet (PK) │
│ RaisonSociale   │   1,n        0,1          │ Intitule        │
│ Adresse         │   demande                 │ DateDebut       │
│ Contact         │                           │ DateFinPrevue   │
└─────────────────┘                           │ Budget          │
                                              └────────┬────────┘
                                                       │
                                                  0,n  │ participe
                                                       │ NbHeures
                                                       │
┌─────────────────────────────────────────────────────┴─────────┐
│                          EMPLOYE                               │
├────────────────────────────────────────────────────────────────┤
│ Matricule (PK)                                                 │
│ Nom                                                            │
│ Prenom                                                         │
│ DateEmbauche                                                   │
│ Poste                                                          │
│ Salaire                                                        │
└────────────────────────────────────────────────────────────────┘
                              │
                         0,n  │ chef_de
                              │
                         0,1  │
                              ↓
                        PROJET (relation réflexive implicite)
```

**Note** : La relation "chef de projet" peut être modélisée comme une clé étrangère dans PROJET pointant vers EMPLOYE.

```
PROJET contient aussi : #MatriculeChefProjet (FK vers EMPLOYE)
```

---

## Exercice 6 : Relations Avancées

### Partie A : Relation Ternaire vs Quaternaire

C'est une relation **QUATERNAIRE** car elle implique 4 entités :
1. PROFESSEUR
2. MATIERE
3. SALLE
4. CRENEAU (ou HORAIRE)

```
┌───────────────┐   ┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│  PROFESSEUR   │   │   MATIERE     │   │    SALLE      │   │   CRENEAU     │
└───────┬───────┘   └───────┬───────┘   └───────┬───────┘   └───────┬───────┘
        │                   │                   │                   │
        └───────────────────┴───────────────────┴───────────────────┘
                                    │
                            ┌───────┴───────┐
                            │   ENSEIGNE    │
                            └───────────────┘
```

### Partie B : Associations Réflexives

**1. Supervision d'employés** :
```
EMPLOYE (0,1) ──supervise── (0,n) EMPLOYE
```

**2. Composition de pièces** :
```
PIECE (0,n) ──compose── (0,n) PIECE
            Quantite
```

**3. Prérequis de cours** :
```
COURS (0,n) ──prerequis── (0,n) COURS
```

### Partie C : Spécialisation

```
              ┌─────────────────┐
              │    PERSONNE     │
              ├─────────────────┤
              │ NumPersonne(PK) │
              │ Nom             │
              │ Prenom          │
              │ Adresse         │
              │ Telephone       │
              └────────┬────────┘
                       │
          ┌────────────┼────────────┐
          │            │            │
   ┌──────┴──────┐ ┌───┴────┐ ┌─────┴─────┐
   │   EMPLOYE   │ │ CLIENT │ │FOURNISSEUR│
   ├─────────────┤ ├────────┤ ├───────────┤
   │ Matricule   │ │NumClient││CodeFourn  │
   │ DateEmbauche│ │ CA     │ │ Conditions│
   │ Salaire     │ │        │ │           │
   └─────────────┘ └────────┘ └───────────┘
```

---

## Exercice 7 : Agence Immobilière

### MCD Complet

```
┌─────────────────┐  0,n        1,n  ┌─────────────────┐
│   PROPRIETAIRE  │──────────────────│      BIEN       │
├─────────────────┤   possede        ├─────────────────┤
│ NumProprio (PK) │                  │ RefBien (PK)    │
│ Nom             │                  │ TypeBien        │
│ Prenom          │                  │ Adresse         │
│ Adresse         │                  │ Surface         │
│ Telephone       │                  │ NbPieces        │
└─────────────────┘                  │ Prix            │
                                     │ Disponible      │
                                     └────────┬────────┘
                                              │
                                         0,n  │ visite
                                              │ DateVisite
                                              │ HeureVisite
                                              │ Commentaires
                                              │
┌─────────────────┐                           │
│     AGENT       │                           │
├─────────────────┤                           │
│ NumAgent (PK)   │◄──────────────────────────┤
│ Nom             │   0,n        1,1          │
│ Prenom          │   accompagne              │
│ Telephone       │                           │
└─────────────────┘                           │
                                              │
                                         0,n  │
                                              │
                                     ┌────────┴────────┐
                                     │     CLIENT      │
                                     ├─────────────────┤
                                     │ NumClient (PK)  │
                                     │ Nom             │
                                     │ Prenom          │
                                     │ Budget          │
                                     │ TypeRecherche   │
                                     └────────┬────────┘
                                              │
                                         0,n  │ realise
                                              │ DateTransaction
                                              │ Montant
                                              │ TypeTransaction
                                              │
                                     ┌────────┴────────┐
                                     │   TRANSACTION   │
                                     ├─────────────────┤
                                     │ NumTransaction  │
                                     │ (association)   │
                                     └─────────────────┘
```

---

## Exercice 8 : Questions de Compréhension

### Question 1 : Différence MCT / MCD
- **MCT** : Modélise les traitements (processus, actions, flux)
- **MCD** : Modélise les données (entités, attributs, relations)
- Complémentaires : le MCT montre QUOI faire, le MCD montre SUR QUOI

### Question 2 : MCD indépendant de la technologie
- Pas de types de données spécifiques
- Pas de contraintes liées à un SGBD
- Représente la réalité métier, pas l'implémentation

### Question 3 : Attributs sur relation N:M
- Quand l'information dépend de la combinaison des deux entités
- Exemple : Note dépend de (Étudiant, Cours), pas de l'un ou l'autre seul

### Question 4 : Identifier si pas en 3FN
- Chercher les dépendances transitives
- Si A → B et B → C où B n'est pas clé, alors pas 3FN

### Question 5 : Utilité pratique de la normalisation
- Évite les erreurs de saisie redondante
- Facilite les mises à jour
- Réduit l'espace de stockage
- Garantit la cohérence des données

---

## Exercice Bonus : Modélisation depuis Formulaire

### Entités Identifiées

1. **CLIENT** : NumClient, Nom, Adresse, Telephone, Email
2. **COMMANDE** : NumCommande, Date, ModePaiement, TypeLivraison
3. **ARTICLE** : Reference, Designation, PrixUnitaire
4. **LIGNE_COMMANDE** : Quantite (+ clés)

### MCD

```
┌─────────────┐  1,n           0,n  ┌─────────────┐
│   CLIENT    │────────────────────│  COMMANDE   │
├─────────────┤      passe         ├─────────────┤
│ NumClient   │                    │ NumCommande │
│ Nom         │                    │ Date        │
│ Adresse     │                    │ ModePaiement│
│ Telephone   │                    │ TypeLivraison│
│ Email       │                    └──────┬──────┘
└─────────────┘                           │
                                     0,n  │ contient
                                          │ Quantite
                                          │
                                   ┌──────┴──────┐
                                   │   ARTICLE   │
                                   ├─────────────┤
                                   │ Reference   │
                                   │ Designation │
                                   │ PrixUnitaire│
                                   └─────────────┘
```
