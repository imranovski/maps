# Exercices Jour 2 - MCT et Modèle Conceptuel de Données (MCD)

## Exercice 1 : Modèle Conceptuel des Traitements (MCT)

### Énoncé
Modélisez les processus suivants avec un MCT.

### Processus 1 : Demande de Congés
1. Un employé fait une demande de congés
2. Le responsable vérifie les jours disponibles
3. Si jours suffisants : la demande est acceptée
4. Sinon : la demande est refusée

**Travail demandé** : Dessinez le MCT complet avec événements, opérations et résultats.

### Processus 2 : Traitement d'une Réclamation Client
1. Le client dépose une réclamation
2. Le service client examine la réclamation
3. Si réclamation fondée : proposition de dédommagement
4. Si réclamation non fondée : rejet avec explication

**Travail demandé** : Dessinez le MCT complet.

### Processus 3 : Inscription à un Examen
1. L'étudiant dépose une demande d'inscription
2. Le secrétariat vérifie les prérequis
3. Si prérequis validés ET frais payés : inscription confirmée
4. Si prérequis non validés : inscription refusée
5. Si frais non payés : demande de paiement

**Travail demandé** : Dessinez le MCT avec synchronisation.

---

## Exercice 2 : Normalisation - Première Forme Normale (1FN)

### Énoncé
Les tables suivantes ne sont pas en 1FN. Corrigez-les.

### Table 1 : EMPLOYE
```
| NumEmploye | Nom    | Telephones              | Competences          |
|------------|--------|-------------------------|----------------------|
| E001       | Dupont | 0612345678, 0698765432  | Java, Python, SQL    |
| E002       | Martin | 0654321098              | Excel, VBA           |
```

### Table 2 : COMMANDE
```
| NumCommande | Client  | Produits                           |
|-------------|---------|-----------------------------------|
| CMD001      | Société A| P001:5, P002:3, P003:10          |
| CMD002      | Société B| P001:2                            |
```

### Table 3 : COURS
```
| CodeCours | Intitule    | Enseignants          | Horaires           |
|-----------|-------------|----------------------|--------------------|
| INF101    | Informatique| M. Dupont, Mme Martin| Lundi 8h, Mercredi 10h |
```

**Travail demandé** : Proposez une version normalisée en 1FN pour chaque table.

---

## Exercice 3 : Normalisation - 2FN et 3FN

### Énoncé
Analysez les tables suivantes et normalisez-les.

### Table 1 : INSCRIPTION (Non 2FN)
```
| NumEtudiant | CodeCours | NomEtudiant | IntituleCours | Note |
|-------------|-----------|-------------|---------------|------|
| E001        | INF101    | Dupont      | Informatique  | 14   |
| E001        | MAT201    | Dupont      | Mathématiques | 16   |
| E002        | INF101    | Martin      | Informatique  | 12   |
```

**Questions** :
1. Quelle est la clé primaire ?
2. Pourquoi n'est-elle pas en 2FN ?
3. Proposez une version en 2FN.

### Table 2 : EMPLOYE (Non 3FN)
```
| NumEmploye | Nom    | CodeService | NomService    | LocalisationService |
|------------|--------|-------------|---------------|---------------------|
| E001       | Dupont | SRV01       | Informatique  | Bâtiment A         |
| E002       | Martin | SRV01       | Informatique  | Bâtiment A         |
| E003       | Durand | SRV02       | Commercial    | Bâtiment B         |
```

**Questions** :
1. Quelle est la dépendance transitive ?
2. Proposez une version en 3FN.

---

## Exercice 4 : Dépendances Fonctionnelles

### Énoncé
Identifiez toutes les dépendances fonctionnelles dans les contextes suivants.

### Contexte 1 : Facture
Attributs : NumFacture, DateFacture, NumClient, NomClient, AdresseClient, MontantTotal

### Contexte 2 : Ligne de Commande
Attributs : NumCommande, RefProduit, Designation, PrixUnitaire, Quantite, MontantLigne

### Contexte 3 : Étudiant
Attributs : NumEtudiant, Nom, Prenom, DateNaissance, CodeClasse, NomClasse, NomProfPrincipal

**Travail demandé** : Listez les DF sous la forme A → B.

---

## Exercice 5 : Création d'un MCD Complet

### Contexte : Gestion de Projet
Une entreprise de conseil souhaite gérer ses projets. Le système doit gérer :

**Les employés** :
- Matricule (identifiant)
- Nom, Prénom
- Date d'embauche
- Poste
- Salaire

**Les projets** :
- Code projet (identifiant)
- Intitulé
- Date début, Date fin prévue
- Budget

**Les clients** :
- Code client (identifiant)
- Raison sociale
- Adresse
- Contact

**Règles de gestion** :
1. Un projet est réalisé pour un et un seul client
2. Un client peut avoir plusieurs projets
3. Un employé peut travailler sur plusieurs projets
4. Un projet peut impliquer plusieurs employés
5. On veut connaître le nombre d'heures travaillées par chaque employé sur chaque projet
6. Chaque projet a un chef de projet (un employé)

**Travail demandé** : Dessinez le MCD complet avec toutes les cardinalités.

---

## Exercice 6 : Relations Avancées

### Partie A : Relation Ternaire
Une université gère l'emploi du temps avec la règle suivante :
"Un professeur enseigne une matière dans une salle à un créneau horaire donné"

**Travail demandé** : Modélisez cette situation. Est-ce une relation ternaire ou quaternaire ?

### Partie B : Association Réflexive
Modélisez les situations suivantes :
1. Un employé peut superviser d'autres employés
2. Une pièce détachée peut être composée d'autres pièces détachées
3. Un cours peut avoir des cours prérequis

### Partie C : Spécialisation
Dans une entreprise, les personnes peuvent être :
- Des employés (avec matricule, date embauche, salaire)
- Des clients (avec numéro client, chiffre affaires)
- Des fournisseurs (avec code fournisseur, conditions paiement)

Toutes les personnes ont : nom, prénom, adresse, téléphone.

**Travail demandé** : Modélisez avec une spécialisation.

---

## Exercice 7 : Étude de Cas - Agence Immobilière

### Contexte
Une agence immobilière gère :

**Les biens immobiliers** :
- Référence, type (appartement, maison, terrain)
- Adresse, surface, nombre de pièces
- Prix, disponibilité

**Les propriétaires** :
- Numéro, nom, prénom
- Adresse, téléphone

**Les clients** (acheteurs/locataires) :
- Numéro, nom, prénom
- Budget, type de bien recherché

**Les visites** :
- Date, heure, commentaires

**Les transactions** (ventes ou locations) :
- Date, montant, type (vente/location)

### Règles de Gestion
1. Un bien appartient à un ou plusieurs propriétaires
2. Un propriétaire peut posséder plusieurs biens
3. Un client peut visiter plusieurs biens
4. Un bien peut être visité par plusieurs clients
5. Une transaction concerne un bien et un client
6. Un agent de l'agence accompagne chaque visite

### Travail Demandé
1. Identifiez toutes les entités et leurs attributs
2. Identifiez toutes les relations avec leurs cardinalités
3. Dessinez le MCD complet
4. Vérifiez la normalisation

---

## Exercice 8 : Questions de Compréhension

### Question 1
Expliquez la différence entre le MCT et le MCD.

### Question 2
Pourquoi dit-on que le MCD est indépendant de la technologie ?

### Question 3
Dans quel cas une relation N:M nécessite-t-elle des attributs propres ?

### Question 4
Comment identifier si une table n'est pas en 3FN ?

### Question 5
Quelle est l'utilité pratique de la normalisation pour un enseignant qui crée une base de données pédagogique ?

---

## Exercice Bonus : Modélisation à Partir d'un Formulaire

### Énoncé
À partir du formulaire suivant, déduisez le MCD.

```
╔══════════════════════════════════════════════════════════╗
║                 FICHE DE COMMANDE                        ║
╠══════════════════════════════════════════════════════════╣
║ N° Commande : ________    Date : __/__/____              ║
║                                                          ║
║ CLIENT :                                                 ║
║ N° Client : ______  Nom : _____________________________  ║
║ Adresse : ____________________________________________   ║
║ Téléphone : ______________  Email : _________________    ║
║                                                          ║
║ ARTICLES COMMANDÉS :                                     ║
║ ┌────────┬────────────────────┬─────────┬────┬─────────┐ ║
║ │ Réf.   │ Désignation        │ Prix U. │ Qté│ Total   │ ║
║ ├────────┼────────────────────┼─────────┼────┼─────────┤ ║
║ │        │                    │         │    │         │ ║
║ │        │                    │         │    │         │ ║
║ │        │                    │         │    │         │ ║
║ └────────┴────────────────────┴─────────┴────┴─────────┘ ║
║                                                          ║
║                        TOTAL COMMANDE : _____________ €  ║
║                                                          ║
║ Mode de paiement : □ CB  □ Chèque  □ Virement            ║
║ Livraison : □ Domicile  □ Point relais                   ║
╚══════════════════════════════════════════════════════════╝
```

**Travail demandé** :
1. Identifiez les entités
2. Identifiez les attributs
3. Dessinez le MCD
