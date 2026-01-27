# Exercices Jour 3 - MCD Approfondissement et MLD

## Exercice 1 : Transformation MCD → MLD - Cas Simples

### Énoncé
Transformez les MCD suivants en MLD.

### Cas 1 : Relation 1:N Simple
```
┌─────────────┐  1,1           1,n  ┌─────────────┐
│  ETUDIANT   │────────────────────│   CLASSE    │
├─────────────┤    appartient      ├─────────────┤
│ NumEtud     │                    │ CodeClasse  │
│ Nom         │                    │ Libelle     │
│ Prenom      │                    │ Niveau      │
└─────────────┘                    └─────────────┘
```

### Cas 2 : Relation N:M Simple
```
┌─────────────┐  0,n           0,n  ┌─────────────┐
│  AUTEUR     │────────────────────│   LIVRE     │
├─────────────┤      ecrit         ├─────────────┤
│ CodeAuteur  │                    │ ISBN        │
│ NomAuteur   │                    │ Titre       │
└─────────────┘                    └─────────────┘
```

### Cas 3 : Relation N:M avec Attributs
```
┌─────────────┐  0,n           0,n  ┌─────────────┐
│  EMPLOYE    │────────────────────│   PROJET    │
├─────────────┤    participe       ├─────────────┤
│ Matricule   │    NbHeures        │ CodeProjet  │
│ NomEmploye  │    Role            │ Intitule    │
└─────────────┘                    └─────────────┘
```

### Cas 4 : Relation 1:1
```
┌─────────────┐  1,1           0,1  ┌─────────────┐
│  PERSONNE   │────────────────────│ PERMIS_COND │
├─────────────┤    possede         ├─────────────┤
│ NumPersonne │                    │ NumPermis   │
│ Nom         │                    │ DateObtention│
│ Prenom      │                    │ Categories  │
└─────────────┘                    └─────────────┘
```

---

## Exercice 2 : Transformation MCD → MLD - Cas Complexes

### Cas 1 : Relation Ternaire
```
            ┌─────────────┐
            │ PROFESSEUR  │
            ├─────────────┤
            │ NumProf     │────┐
            │ NomProf     │    │ 0,n
            └─────────────┘    │
                               │
                          ┌────┴────┐
                          │ENSEIGNE │
                          │NbHeures │
                          └────┬────┘
                          /         \
                    0,n  /           \  0,n
                        /             \
          ┌─────────────┐           ┌─────────────┐
          │   MATIERE   │           │   CLASSE    │
          ├─────────────┤           ├─────────────┤
          │ CodeMatiere │           │ CodeClasse  │
          │ LibMatiere  │           │ NomClasse   │
          └─────────────┘           └─────────────┘
```

**Travail demandé** : Transformez en MLD et identifiez la clé primaire de la table associative.

### Cas 2 : Association Réflexive
```
┌─────────────┐
│   EMPLOYE   │
├─────────────┤
│ Matricule   │◄──────┐
│ NomEmploye  │       │ supervise
│ Prenom      │───────┘
│ Poste       │   0,n      0,1
└─────────────┘
```

**Travail demandé** : Transformez en MLD.

### Cas 3 : Double Relation entre Entités
```
┌─────────────┐                    ┌─────────────┐
│   CLIENT    │    0,n             │   ADRESSE   │
├─────────────┤────────────────────├─────────────┤
│ NumClient   │  adresse_livraison │ CodeAdresse │
│ NomClient   │    0,1             │ Rue         │
│             │                    │ Ville       │
│             │    0,n             │ CodePostal  │
│             │────────────────────│             │
│             │ adresse_facturation│             │
│             │    0,1             │             │
└─────────────┘                    └─────────────┘
```

**Travail demandé** : Transformez en MLD.

---

## Exercice 3 : Transformation Complète

### Énoncé
Transformez le MCD suivant en MLD.

```
┌─────────────────┐                           ┌─────────────────┐
│     CLIENT      │                           │   CATEGORIE     │
├─────────────────┤                           ├─────────────────┤
│ NumClient       │                           │ CodeCategorie   │
│ NomClient       │                           │ LibCategorie    │
│ Adresse         │                           └────────┬────────┘
│ Email           │                                    │ 1,n
│ Telephone       │                                    │
└────────┬────────┘                               ┌────┴────┐
         │ 1,n                                    │ classe  │
         │                                        └────┬────┘
    ┌────┴────┐                                        │ 0,n
    │  passe  │                                        │
    └────┬────┘                              ┌─────────┴─────────┐
         │ 0,n                               │      PRODUIT      │
         │                                   ├───────────────────┤
┌────────┴────────┐                          │ RefProduit        │
│    COMMANDE     │                          │ Designation       │
├─────────────────┤                          │ PrixUnitaire      │
│ NumCommande     │                          │ Stock             │
│ DateCommande    │◄─────────────────────────┤                   │
│ Statut          │  0,n  contient    0,n    │                   │
│ MontantTotal    │       Quantite           │                   │
└─────────────────┘                          └───────────────────┘
```

**Travail demandé** :
1. Listez toutes les tables
2. Définissez les clés primaires
3. Identifiez les clés étrangères
4. Écrivez le MLD complet

---

## Exercice 4 : Vérification de Cohérence

### Énoncé
Le MLD suivant contient des erreurs. Identifiez-les et corrigez.

```
CLIENT (NumClient, NomClient, Adresse)
COMMANDE (NumCommande, DateCommande, NomClient, Adresse)
PRODUIT (RefProduit, Designation, PrixUnitaire)
LIGNE_COMMANDE (RefProduit, Quantite, PrixUnitaire, Designation)
```

**Questions** :
1. Quelles sont les erreurs de redondance ?
2. Quelles clés étrangères manquent ?
3. Quelle clé primaire est incomplète ?
4. Proposez un MLD corrigé.

---

## Exercice 5 : Du MLD vers le Dictionnaire de Données

### Énoncé
À partir du MLD suivant, créez le dictionnaire de données.

```
EMPLOYE (Matricule, Nom, Prenom, DateEmbauche, Salaire, #CodeService)
SERVICE (CodeService, NomService, Localisation)
PROJET (CodeProjet, Intitule, DateDebut, DateFin, Budget)
PARTICIPATION (#Matricule, #CodeProjet, NbHeures, Role)
```

**Format du dictionnaire** :

| Table | Champ | Type | Taille | Clé | Obligatoire | Description |
|-------|-------|------|--------|-----|-------------|-------------|
| ... | ... | ... | ... | ... | ... | ... |

---

## Exercice 6 : Analyse et Critique de MLD

### Énoncé
Analysez le MLD suivant et répondez aux questions.

```
ETUDIANT (NumEtudiant, NomEtudiant, PrenomEtudiant, DateNaissance, 
          AdresseRue, AdresseVille, AdresseCP, Email, Telephone,
          #CodeClasse, NomClasse)

CLASSE (CodeClasse, NomClasse, Niveau, Annee, #NumProfPrincipal, NomProf)

PROFESSEUR (NumProf, NomProf, PrenomProf, Email, #CodeMatiere, LibMatiere)

MATIERE (CodeMatiere, LibMatiere, Coefficient)

NOTE (NumEtudiant, CodeMatiere, Valeur, DateEvaluation, TypeEval)
```

**Questions** :
1. Ce MLD est-il en 3FN ? Justifiez.
2. Identifiez les redondances.
3. Proposez un MLD optimisé.

---

## Exercice 7 : Cas Pratique - Gestion Hospitalière

### Contexte
Un hôpital souhaite gérer :
- Les patients et leurs séjours
- Les médecins et leurs spécialités
- Les chambres et leur occupation
- Les actes médicaux réalisés

### MCD à Transformer

```
┌─────────────────┐                    ┌─────────────────┐
│     PATIENT     │                    │    MEDECIN      │
├─────────────────┤                    ├─────────────────┤
│ NumPatient      │                    │ NumMedecin      │
│ NomPatient      │                    │ NomMedecin      │
│ DateNaissance   │                    │ Specialite      │
│ NumSecu         │                    └────────┬────────┘
└────────┬────────┘                             │
         │                                 0,n  │ realise
    0,n  │ occupe                               │
         │ DateEntree                     ┌─────┴─────┐
         │ DateSortie                     │   ACTE    │
         │                                ├───────────┤
┌────────┴────────┐                       │ CodeActe  │
│     CHAMBRE     │                       │ LibActe   │
├─────────────────┤                       │ Tarif     │
│ NumChambre      │                       └─────┬─────┘
│ TypeChambre     │                             │
│ Etage           │                        0,n  │
└─────────────────┘                             │
         ↑                                      │
    0,n  │                               ┌──────┴──────┐
         └───────────────────────────────│   SEJOUR    │
                  est_dans               ├─────────────┤
                  DateDebut              │ NumSejour   │
                                         │ Motif       │
                                         └─────────────┘
```

**Note** : Un séjour concerne un patient, une chambre, et peut inclure plusieurs actes réalisés par des médecins.

**Travail demandé** :
1. Complétez le MCD avec les relations manquantes
2. Transformez en MLD
3. Identifiez toutes les clés

---

## Exercice 8 : Optimisation

### Énoncé
Le MLD suivant a été conçu pour une application de e-commerce à fort trafic. Proposez des optimisations.

```
CLIENT (IdClient, Nom, Prenom, Email, MotDePasse, DateInscription, 
        DerniereConnexion, NbCommandes, MontantTotalAchats)

COMMANDE (IdCommande, DateCommande, #IdClient, Statut, MontantHT, 
          MontantTVA, MontantTTC, AdresseLivraison, AdresseFacturation)

LIGNE_COMMANDE (#IdCommande, #IdProduit, Quantite, PrixUnitaire, 
                MontantLigne, DesignationProduit)

PRODUIT (IdProduit, Designation, Description, PrixVente, #IdCategorie,
         NomCategorie, Stock, NbVentes)
```

**Questions** :
1. Identifiez les données calculées ou dérivées
2. Identifiez les redondances acceptables pour la performance
3. Quels index recommanderiez-vous ?

---

## Exercice 9 : Questions Théoriques

### Question 1
Expliquez pourquoi une relation 1:N ne génère pas de table supplémentaire en MLD.

### Question 2
Dans quel cas choisirait-on de fusionner deux entités liées par une relation 1:1 ?

### Question 3
Comment gère-t-on une entité faible lors de la transformation en MLD ?

### Question 4
Quelle est la différence entre une clé naturelle et une clé artificielle ? Donnez des exemples.

### Question 5
Expliquez l'impact d'une clé étrangère nullable sur l'intégrité des données.

---

## Exercice Bonus : Rétro-Ingénierie

### Énoncé
À partir du MLD suivant, reconstituez le MCD d'origine.

```
AUTEUR (IdAuteur, NomAuteur, PaysOrigine)
EDITEUR (IdEditeur, NomEditeur, Ville)
LIVRE (ISBN, Titre, AnneePublication, Prix, #IdEditeur)
ECRIT_PAR (#IdAuteur, #ISBN, RoleAuteur)
EXEMPLAIRE (IdExemplaire, #ISBN, DateAcquisition, Etat, #IdBibliotheque)
BIBLIOTHEQUE (IdBibliotheque, NomBib, Adresse)
ADHERENT (IdAdherent, Nom, Prenom, DateAdhesion, #IdBibliotheque)
EMPRUNT (#IdAdherent, #IdExemplaire, DateEmprunt, DateRetourPrevue, DateRetourEffective)
```

**Travail demandé** :
1. Dessinez le MCD correspondant
2. Identifiez les cardinalités
3. Vérifiez la cohérence de votre modèle
