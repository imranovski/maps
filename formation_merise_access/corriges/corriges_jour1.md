# Corrigés Jour 1 - Introduction à Merise et Modélisation E/A

## Exercice 1 : Identification d'Entités et Attributs

### Contexte 1 : Agence de Voyage

**Entités identifiées** :

```
┌─────────────────────┐
│       VOYAGE        │
├─────────────────────┤
│ CodeVoyage (PK)     │
│ Destination         │
│ DateDepart          │
│ DateRetour          │
│ Prix                │
│ NbPlaces            │
└─────────────────────┘

┌─────────────────────┐
│       CLIENT        │
├─────────────────────┤
│ NumClient (PK)      │
│ Nom                 │
│ Prenom              │
│ Adresse             │
│ Telephone           │
│ Email               │
└─────────────────────┘

┌─────────────────────┐
│    RESERVATION      │
├─────────────────────┤
│ NumReservation (PK) │
│ DateReservation     │
│ NbPersonnes         │
│ MontantTotal        │
│ Statut              │
└─────────────────────┘
```

### Contexte 2 : Cabinet Médical

```
┌─────────────────────┐
│       MEDECIN       │
├─────────────────────┤
│ NumMedecin (PK)     │
│ Nom                 │
│ Prenom              │
│ Specialite          │
│ Telephone           │
└─────────────────────┘

┌─────────────────────┐
│       PATIENT       │
├─────────────────────┤
│ NumPatient (PK)     │
│ Nom                 │
│ Prenom              │
│ DateNaissance       │
│ Adresse             │
│ NumSecu             │
└─────────────────────┘

┌─────────────────────┐
│    CONSULTATION     │
├─────────────────────┤
│ NumConsult (PK)     │
│ DateHeure           │
│ Motif               │
│ Diagnostic          │
│ Prescription        │
└─────────────────────┘
```

### Contexte 3 : Location de Véhicules

```
┌─────────────────────┐
│      VEHICULE       │
├─────────────────────┤
│ Immatriculation(PK) │
│ Marque              │
│ Modele              │
│ Annee               │
│ Kilometrage         │
│ TarifJournalier     │
└─────────────────────┘

┌─────────────────────┐
│       CLIENT        │
├─────────────────────┤
│ NumClient (PK)      │
│ Nom                 │
│ Prenom              │
│ PermisNumero        │
│ Telephone           │
│ Email               │
└─────────────────────┘

┌─────────────────────┐
│      LOCATION       │
├─────────────────────┤
│ NumLocation (PK)    │
│ DateDebut           │
│ DateFin             │
│ KmDepart            │
│ KmRetour            │
│ MontantTotal        │
└─────────────────────┘
```

---

## Exercice 2 : Détermination des Cardinalités

### Situation 1
EMPLOYE **(1,1)** appartient **(1,n)** DEPARTEMENT

*Un employé appartient à un et un seul département. Un département a au moins un employé.*

### Situation 2
CLIENT **(0,n)** passe **(1,1)** COMMANDE

*Un client peut passer zéro ou plusieurs commandes. Une commande est passée par un et un seul client.*

### Situation 3
ETUDIANT **(0,n)** inscrit **(0,n)** COURS

*Relation plusieurs à plusieurs : un étudiant peut s'inscrire à plusieurs cours, un cours peut avoir plusieurs étudiants.*

### Situation 4
LIVRE **(1,n)** écrit **(0,n)** AUTEUR

*Un livre a au moins un auteur (peut en avoir plusieurs). Un auteur peut avoir écrit zéro ou plusieurs livres.*

### Situation 5
EMPLOYE **(0,1)** occupe **(0,1)** BUREAU

*Relation un à un optionnelle : un employé peut avoir au maximum un bureau, un bureau peut être attribué à au maximum un employé.*

---

## Exercice 3 : Lecture d'un Modèle E/A

### Réponses

1. **Combien de catégories un véhicule peut-il avoir ?**
   - Une et une seule catégorie (cardinalité 1,1 côté VEHICULE)

2. **Un client peut-il effectuer plusieurs locations ?**
   - Oui (cardinalité 0,n côté CLIENT)

3. **Un véhicule peut-il faire l'objet de plusieurs locations ?**
   - Oui (cardinalité 0,n côté VEHICULE vers LOCATION)

4. **Quels attributs caractérisent la relation "fait l'objet" ?**
   - DateDebut, DateFin, KmDebut, KmFin

5. **Quel est l'identifiant de l'entité VEHICULE ?**
   - Immatriculation

---

## Exercice 4 : Modélisation Complète - Club de Sport

### MCD Complet

```
┌─────────────────┐                           ┌─────────────────┐
│    ADHERENT     │                           │      COACH      │
├─────────────────┤                           ├─────────────────┤
│ NumAdherent(PK) │                           │ NumCoach (PK)   │
│ Nom             │                           │ Nom             │
│ Prenom          │                           │ Prenom          │
│ DateNaissance   │                           │ Specialite      │
│ Adresse         │                           │ Telephone       │
│ Telephone       │                           └────────┬────────┘
│ DateAdhesion    │                                    │
└────────┬────────┘                                    │ 1,n
         │                                             │
    0,n  │ s'inscrit                              ┌────┴────┐
         │ DateInscription                        │ encadre │
         │                                        └────┬────┘
         │                                             │ 0,1
         │                                             │
    ┌────┴────────────────────────────────────────────┴────┐
    │                      ACTIVITE                         │
    ├───────────────────────────────────────────────────────┤
    │ CodeActivite (PK)                                     │
    │ NomActivite                                           │
    │ Description                                           │
    │ NiveauRequis                                          │
    └─────────────────────────────┬─────────────────────────┘
                                  │
                             1,n  │ concerne
                                  │
                            ┌─────┴─────┐
                            │  SEANCE   │
                            ├───────────┤
                            │ NumSeance │
                            │ Date      │
                            │ Heure     │
                            │ Duree     │
                            │ Salle     │
                            └───────────┘
```

---

## Exercice 5 : Correction d'Erreurs

### Erreurs Identifiées

1. **NomFournisseur dans PRODUIT** : Redondance, cette information est déjà dans FOURNISSEUR
2. **Produits dans FOURNISSEUR** : Attribut multivalué, viole la 1FN
3. **Cardinalité (0,n) côté PRODUIT** : Signifie qu'un produit peut ne pas avoir de fournisseur, à vérifier
4. **Cardinalité (1,n) côté FOURNISSEUR** : Signifie qu'un fournisseur fournit au moins un produit

### Modèle Corrigé

```
┌─────────────────┐  0,n        1,n  ┌─────────────────┐
│    PRODUIT      │──────────────────│   FOURNISSEUR   │
├─────────────────┤   fournit        ├─────────────────┤
│ RefProduit (PK) │   PrixAchat      │ CodeFournisseur │
│ Designation     │   DelaiLivraison │ RaisonSociale   │
│ PrixVente       │                  │ Adresse         │
│ Stock           │                  │ Email           │
└─────────────────┘                  │ Telephone       │
                                     └─────────────────┘
```

---

## Exercice 6 : Cas Pratique - Restaurant

### Entités et Attributs

```
┌─────────────────┐
│      PLAT       │
├─────────────────┤
│ CodePlat (PK)   │
│ NomPlat         │
│ Description     │
│ Prix            │
│ Categorie       │
│ Disponible      │
└─────────────────┘

┌─────────────────┐
│   INGREDIENT    │
├─────────────────┤
│ CodeIngredient  │
│ NomIngredient   │
│ Unite           │
│ StockActuel     │
│ Allergene       │
└─────────────────┘

┌─────────────────┐
│     CLIENT      │
├─────────────────┤
│ NumClient (PK)  │
│ Nom             │
│ Prenom          │
│ Telephone       │
│ Email           │
└─────────────────┘

┌─────────────────┐
│      TABLE      │
├─────────────────┤
│ NumTable (PK)   │
│ Capacite        │
│ Emplacement     │
│ Statut          │
└─────────────────┘

┌─────────────────┐
│   RESERVATION   │
├─────────────────┤
│ NumReservation  │
│ DateHeure       │
│ NbPersonnes     │
│ Statut          │
└─────────────────┘

┌─────────────────┐
│    COMMANDE     │
├─────────────────┤
│ NumCommande (PK)│
│ DateHeure       │
│ Statut          │
│ MontantTotal    │
└─────────────────┘
```

### MCD Complet

```
                PLAT 0,n ── compose (Quantite) ── 1,n INGREDIENT
                  │
             0,n  │ contient
                  │ Quantite
                  │
    CLIENT ── passe ── COMMANDE ── concerne ── TABLE
     1,n       0,n       1,1          0,n       0,n
       │
  0,n  │ effectue
       │
  RESERVATION ── reserve ── TABLE
       0,n           0,n     0,n
```

---

## Exercice 7 : Questions de Réflexion

### Question 1
**Pourquoi définir un identifiant pour chaque entité ?**
- Permet d'identifier de manière unique chaque occurrence
- Évite les doublons
- Sert de référence pour les relations (clés étrangères)
- Nécessaire pour la mise à jour et la suppression

### Question 2
**Quand une relation a-t-elle des attributs propres ?**
- Quand l'information caractérise la relation, pas les entités
- Exemple : Date d'emprunt dans la relation EMPRUNTE entre ADHERENT et LIVRE
- Fréquent dans les relations N:M

### Question 3
**Différence entre (0,n) et (1,n)**
- (0,n) : Participation optionnelle, une occurrence peut ne pas participer à la relation
- (1,n) : Participation obligatoire, au moins une participation

### Question 4
**Modéliser un supérieur hiérarchique**
- Association réflexive sur EMPLOYE
- Relation "supervise" ou "dirige"
- Cardinalités : (0,1) côté subordonné, (0,n) côté supérieur

```
EMPLOYE ──(supervise 0,1 - 0,n)── EMPLOYE
```

---

## Exercice Bonus : Analyse de Situation Scolaire

### Entités Identifiées

1. ELEVE
2. CLASSE
3. PROFESSEUR
4. MATIERE
5. NOTE

### MCD Proposé

```
┌───────────────┐  1,1           1,n  ┌───────────────┐
│     ELEVE     │─────────────────────│    CLASSE     │
├───────────────┤    appartient       ├───────────────┤
│ NumEleve (PK) │                     │ CodeClasse    │
│ Nom           │                     │ Libelle       │
│ Prenom        │                     │ Niveau        │
└───────┬───────┘                     └───────┬───────┘
        │                                     │
   0,n  │ obtient                        0,1  │ a_pour_pp
        │ Note                                │
        │ DateEval                            │
        │                                     │
        │                              ┌──────┴──────┐
        │                              │ PROFESSEUR  │
        │                              ├─────────────┤
        │                              │ NumProf(PK) │
        │                              │ Nom         │
        │                              │ Prenom      │
        │                              └──────┬──────┘
        │                                     │
        │                                0,n  │ enseigne
        │                                     │
        └──────────────────┬──────────────────┘
                           │
                    ┌──────┴──────┐
                    │   MATIERE   │
                    ├─────────────┤
                    │ CodeMat(PK) │
                    │ Libelle     │
                    │ Coefficient │
                    └─────────────┘
```

**Discussion des choix** :
- Relation ternaire possible entre ELEVE, MATIERE et NOTE
- Le professeur principal est une relation 1:1 avec CLASSE
- L'enseignement est une relation N:M entre PROFESSEUR et MATIERE
