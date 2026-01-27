# Exercices Jour 4 - MPD et MS Access

## Exercice 1 : Définition des Types de Données

### Énoncé
Pour chaque attribut, choisissez le type de données MS Access le plus approprié.

| Attribut | Type Access | Taille/Format | Justification |
|----------|-------------|---------------|---------------|
| NuméroClient | | | |
| NomClient | | | |
| DateNaissance | | | |
| Email | | | |
| Salaire | | | |
| QuantitéStock | | | |
| Actif (oui/non) | | | |
| Photo | | | |
| Description longue | | | |
| CodePostal | | | |
| Téléphone | | | |
| SiteWeb | | | |
| NuméroSécuritéSociale | | | |
| PrixUnitaire | | | |

---

## Exercice 2 : Création du MPD

### Énoncé
À partir du MLD suivant, créez le MPD pour MS Access.

```
ETUDIANT (NumEtud, Nom, Prenom, DateNaissance, Email, Telephone, #CodeClasse)
CLASSE (CodeClasse, NomClasse, Niveau, Annee)
MATIERE (CodeMatiere, Libelle, Coefficient)
NOTE (#NumEtud, #CodeMatiere, Valeur, DateEvaluation, Appreciation)
```

### Format du MPD

Pour chaque table, définissez :
- Nom du champ
- Type de données
- Taille
- Clé primaire/étrangère
- Obligatoire (Oui/Non)
- Valeur par défaut
- Règle de validation
- Message d'erreur

---

## Exercice 3 : Masques de Saisie

### Énoncé
Créez les masques de saisie pour les champs suivants.

1. **Code Postal français** : 5 chiffres obligatoires
2. **Numéro de téléphone** : Format 00 00 00 00 00
3. **Numéro SIRET** : Format 000 000 000 00000
4. **Code ISBN** : Format 000-0-00-000000-0
5. **Immatriculation** : Format AA-000-AA
6. **Date** : Format JJ/MM/AAAA

### Format de Réponse
| Champ | Masque de saisie | Exemple |
|-------|------------------|---------|
| CodePostal | | |

---

## Exercice 4 : Règles de Validation

### Énoncé
Écrivez les règles de validation pour les contraintes suivantes.

1. Le prix doit être supérieur à 0
2. La quantité doit être entre 0 et 9999
3. La date de commande ne peut pas être dans le futur
4. L'email doit contenir un @
5. Le statut doit être "En cours", "Livré" ou "Annulé"
6. La date de fin doit être postérieure à la date de début
7. Le code doit commencer par une lettre
8. La note doit être entre 0 et 20

### Format de Réponse
| Contrainte | Règle de validation | Message d'erreur |
|------------|---------------------|------------------|
| Prix > 0 | | |

---

## Exercice 5 : Travaux Pratiques Access - Création de Tables

### Partie A : Table CLIENT

Créez la table tblClient avec les spécifications suivantes :

| Champ | Type | Propriétés |
|-------|------|------------|
| NumClient | NuméroAuto | Clé primaire |
| RaisonSociale | Texte(100) | Obligatoire |
| Adresse | Texte(200) | |
| CodePostal | Texte(5) | Masque: 00000 |
| Ville | Texte(50) | |
| Telephone | Texte(14) | Masque: 00\ 00\ 00\ 00\ 00 |
| Email | Texte(100) | Validation: Like "*@*.*" |
| DateCreation | Date/Heure | Par défaut: Date() |
| Actif | Oui/Non | Par défaut: Oui |

### Partie B : Table PRODUIT

Créez la table tblProduit :

| Champ | Type | Propriétés |
|-------|------|------------|
| RefProduit | Texte(10) | Clé primaire, Format: >LL-0000 |
| Designation | Texte(100) | Obligatoire |
| Description | Mémo | |
| PrixAchat | Monétaire | Validation: >= 0 |
| PrixVente | Monétaire | Validation: > [PrixAchat] |
| QuantiteStock | Entier | Par défaut: 0, Validation: >= 0 |
| SeuilAlerte | Entier | Par défaut: 10 |
| CodeCategorie | Texte(5) | Clé étrangère |
| DateCreation | Date/Heure | Par défaut: Date() |

### Partie C : Table COMMANDE

Créez la table tblCommande :

| Champ | Type | Propriétés |
|-------|------|------------|
| NumCommande | NuméroAuto | Clé primaire |
| DateCommande | Date/Heure | Obligatoire, Par défaut: Date() |
| NumClient | Entier long | Clé étrangère, Obligatoire |
| Statut | Texte(20) | Validation: In("En cours","Expédié","Livré","Annulé") |
| MontantHT | Monétaire | |
| TauxRemise | Réel simple | Validation: Between 0 And 0.5 |
| Commentaire | Mémo | |

---

## Exercice 6 : Import de Données

### Énoncé
Vous disposez d'un fichier Excel contenant des données clients. Décrivez les étapes pour l'importer dans Access.

### Données Excel (produits.xlsx)

| Reference | Nom_Produit | Prix | Stock | Categorie |
|-----------|-------------|------|-------|-----------|
| PRD001 | Stylo bleu | 1.50 | 500 | Fournitures |
| PRD002 | Cahier A4 | 3.99 | 200 | Fournitures |
| PRD003 | Calculatrice | 15.99 | 50 | Électronique |

### Questions
1. Quelles vérifications faire avant l'import ?
2. Comment gérer les types de données ?
3. Que faire si une colonne contient des erreurs ?

---

## Exercice 7 : Export de Données

### Énoncé
Décrivez les étapes pour exporter des données Access vers :

1. Un fichier Excel (.xlsx)
2. Un fichier CSV
3. Un fichier PDF (pour un état)

### Questions
1. Quelles options d'export choisir pour conserver la mise en forme ?
2. Comment exporter une requête plutôt qu'une table ?
3. Comment automatiser un export régulier ?

---

## Exercice 8 : Cas Pratique Complet

### Contexte
Créez une base de données pour une petite bibliothèque.

### Tables à Créer

**tblLivre**
- ISBN (clé primaire, texte 13)
- Titre (obligatoire)
- Auteur
- Editeur
- AnneePublication (validation: entre 1900 et année en cours)
- NbExemplaires (entier, >= 1)
- Categorie (liste: Roman, BD, Manuel, Documentaire)

**tblAdherent**
- NumAdherent (NuméroAuto, clé primaire)
- Nom (obligatoire)
- Prenom (obligatoire)
- DateNaissance
- Email (unique)
- Telephone (masque de saisie)
- DateInscription (par défaut: date du jour)
- TypeAdherent (Étudiant, Enseignant, Externe)

**tblEmprunt**
- NumEmprunt (NuméroAuto)
- ISBN (clé étrangère)
- NumAdherent (clé étrangère)
- DateEmprunt (par défaut: date du jour)
- DateRetourPrevue (calculée: DateEmprunt + 21 jours)
- DateRetourEffective
- Statut (En cours, Retourné, En retard)

### Travail Demandé
1. Créez les trois tables dans Access
2. Définissez toutes les propriétés
3. Saisissez 5 livres, 3 adhérents et 2 emprunts

---

## Exercice 9 : Questions de Réflexion

### Question 1
Pourquoi utilise-t-on un type Texte pour les codes postaux plutôt qu'un type Numérique ?

### Question 2
Quels sont les avantages et inconvénients d'utiliser NuméroAuto comme clé primaire ?

### Question 3
Comment gérer un champ qui peut contenir plusieurs valeurs (comme les compétences d'un employé) ?

### Question 4
Quelle est la différence entre un champ Obligatoire et un champ Indexé ?

### Question 5
Dans quel cas utiliserait-on un champ Calculé plutôt qu'un champ normal ?

---

## Exercice 10 : Défi - Base de Données Complète

### Énoncé
Créez une base de données complète pour un magasin de vêtements.

### Entités à Gérer
- Articles (référence, désignation, taille, couleur, prix, stock)
- Catégories (code, libellé)
- Clients (numéro, nom, prénom, adresse, fidélité)
- Ventes (numéro, date, client, montant)
- Lignes de vente (vente, article, quantité, prix)

### Travail Demandé
1. Dessinez le MCD
2. Transformez en MLD
3. Créez le MPD
4. Implémentez dans Access
5. Saisissez des données de test
6. Vérifiez que tout fonctionne

---

## Ressources Utiles

### Types de Données Access

| Type | Taille | Utilisation |
|------|--------|-------------|
| Texte court | 0-255 caractères | Noms, codes |
| Texte long | Jusqu'à 1 Go | Descriptions |
| Numéro (Octet) | 0 à 255 | Petits nombres |
| Numéro (Entier) | -32 768 à 32 767 | Nombres moyens |
| Numéro (Entier long) | -2 milliards à 2 milliards | Grands nombres |
| Numéro (Réel simple) | 7 décimales | Calculs simples |
| Numéro (Réel double) | 15 décimales | Calculs précis |
| NuméroAuto | Automatique | Clés primaires |
| Monétaire | 4 décimales | Montants |
| Date/Heure | 8 octets | Dates et heures |
| Oui/Non | 1 bit | Cases à cocher |

### Opérateurs de Validation

| Opérateur | Exemple | Description |
|-----------|---------|-------------|
| = | ="Paris" | Égal à |
| <> | <>"Annulé" | Différent de |
| > < >= <= | >0 | Comparaison |
| Between...And | Between 1 And 100 | Intervalle |
| In() | In("A","B","C") | Liste de valeurs |
| Like | Like "A*" | Correspondance |
| Is Null | Is Null | Valeur nulle |
