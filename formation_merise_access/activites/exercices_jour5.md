# Exercices Jour 5 - MS Access Avancé et Projet Final

## Exercice 1 : Création de Relations

### Partie A : Relations 1:N
Créez les relations suivantes dans votre base de données :

1. **Client → Commande** (Un client peut avoir plusieurs commandes)
2. **Categorie → Produit** (Une catégorie contient plusieurs produits)
3. **Commande → LigneCommande** (Une commande a plusieurs lignes)

### Configuration
- Activez l'intégrité référentielle
- Activez la mise à jour en cascade
- N'activez PAS la suppression en cascade (expliquez pourquoi)

### Partie B : Relations N:M
Créez la relation entre Produit et Fournisseur (un produit peut avoir plusieurs fournisseurs, un fournisseur peut fournir plusieurs produits).

**Tables à créer** :
- tblFournisseur (CodeFournisseur, RaisonSociale, Adresse, Telephone)
- tblFournit (CodeFournisseur, RefProduit, PrixAchat, DelaiLivraison)

---

## Exercice 2 : Requêtes de Sélection

### Requêtes à Créer

1. **qryListeProduits** : Tous les produits avec leur catégorie
2. **qryProduitsEnStock** : Produits dont le stock > 0
3. **qryProduitsAlerte** : Produits dont le stock < seuil d'alerte
4. **qryClientsParVille** : Clients groupés par ville
5. **qryCommandesRecentes** : Commandes des 30 derniers jours

### Format SQL à Fournir
Pour chaque requête, écrivez le code SQL correspondant.

---

## Exercice 3 : Requêtes avec Critères

### Critères Simples

1. Produits dont le prix > 50€
```sql
-- Écrivez la requête
```

2. Clients de Paris ou Lyon
```sql
-- Écrivez la requête
```

3. Commandes du mois en cours
```sql
-- Écrivez la requête
```

### Critères Avancés

4. Produits commençant par "A" et prix entre 10 et 100€
```sql
-- Écrivez la requête
```

5. Clients ayant passé au moins une commande
```sql
-- Écrivez la requête
```

6. Produits jamais commandés
```sql
-- Écrivez la requête
```

---

## Exercice 4 : Requêtes Multi-Tables

### Jointures Internes

1. **Liste des commandes avec nom du client**
```sql
SELECT c.NomClient, cmd.NumCommande, cmd.DateCommande
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient;
```

Créez les requêtes suivantes :

2. **Lignes de commande avec désignation produit**
3. **Commandes avec détail complet (client, produits, quantités)**
4. **Produits avec nom de catégorie**

### Jointures Externes

5. **Clients avec ou sans commandes**
```sql
-- Utilisez LEFT JOIN
```

6. **Produits avec ou sans ventes**
```sql
-- Utilisez LEFT JOIN
```

---

## Exercice 5 : Requêtes Paramétrées

### Créez les requêtes paramétrées suivantes :

1. **qryCommandesClient** : Demande le nom du client
   - Paramètre : [Entrez le nom du client]

2. **qryCommandesPeriode** : Demande une période
   - Paramètres : [Date début] et [Date fin]

3. **qryProduitsCategorie** : Demande la catégorie
   - Paramètre : [Choisissez une catégorie]

4. **qryProduitsRecherche** : Recherche dans la désignation
   - Paramètre : [Rechercher] avec Like "*" & [Rechercher] & "*"

---

## Exercice 6 : Champs Calculés

### Créez les champs calculés suivants :

1. **Montant ligne** : Quantite * PrixUnitaire
```
MontantLigne: [Quantite]*[PrixUnitaire]
```

2. **Montant TTC** : MontantHT * (1 + TauxTVA)
```
-- Écrivez l'expression
```

3. **Nom complet** : Prénom + " " + Nom
```
-- Écrivez l'expression
```

4. **Âge** : Calculé à partir de la date de naissance
```
-- Utilisez DateDiff
```

5. **Statut stock** : "Alerte" si stock < seuil, sinon "OK"
```
-- Utilisez IIf
```

6. **Ancienneté client** : Nombre d'années depuis l'inscription
```
-- Utilisez DateDiff
```

---

## Exercice 7 : Fonctions d'Agrégation

### Créez les requêtes avec agrégation :

1. **Nombre total de produits**
```sql
SELECT COUNT(*) AS NbProduits FROM tblProduit;
```

2. **Nombre de produits par catégorie**
```sql
-- Utilisez GROUP BY
```

3. **Chiffre d'affaires total**
```sql
-- Utilisez SUM sur les montants des commandes
```

4. **CA par client**
```sql
-- GROUP BY client
```

5. **Prix moyen par catégorie**
```sql
-- Utilisez AVG
```

6. **Clients ayant commandé plus de 5 fois**
```sql
-- Utilisez HAVING COUNT(*) > 5
```

---

## Exercice 8 : Requêtes Action

### ⚠️ ATTENTION : Sauvegardez votre base avant ces exercices !

### Requête de Mise à Jour

1. **Augmenter les prix de 5%**
```sql
UPDATE tblProduit
SET PrixVente = [PrixVente] * 1.05;
```

2. **Mettre à jour le statut des commandes anciennes**
```sql
-- Passez en "Archivé" les commandes de plus d'un an
```

### Requête d'Ajout

3. **Copier les produits épuisés vers une table d'archive**
```sql
INSERT INTO tblProduitArchive (RefProduit, Designation, DateArchivage)
SELECT RefProduit, Designation, Date()
FROM tblProduit
WHERE QuantiteStock = 0;
```

### Requête de Suppression

4. **Supprimer les clients inactifs**
```sql
-- Supprimez les clients sans commande depuis plus de 2 ans
-- ⚠️ Vérifiez d'abord avec une requête SELECT
```

---

## Exercice 9 : Mode SQL

### Écrivez en SQL pur les requêtes suivantes :

1. **Sélection avec tri**
```sql
SELECT Designation, PrixVente
FROM tblProduit
WHERE QuantiteStock > 0
ORDER BY PrixVente DESC;
```

2. **Jointure avec alias**
```sql
-- Liste des commandes avec client et total
```

3. **Sous-requête**
```sql
-- Produits dont le prix est supérieur à la moyenne
```

4. **Union**
```sql
-- Combinez clients et fournisseurs dans une liste de contacts
```

---

## Exercice 10 : Projet Final Guidé

### Contexte : Gestion d'une École de Musique

### Étape 1 : Conception (MCD)

Entités à modéliser :
- **ELEVE** : NumEleve, Nom, Prenom, DateNaissance, Adresse, Telephone, Email
- **PROFESSEUR** : NumProf, Nom, Prenom, Specialite, Telephone
- **INSTRUMENT** : CodeInstrument, LibelleInstrument, Famille
- **COURS** : NumCours, Jour, Heure, Salle, Duree
- **INSCRIPTION** : Date, Niveau, Tarif

### Étape 2 : Transformation (MLD)

Transformez le MCD en MLD avec les clés primaires et étrangères.

### Étape 3 : Implémentation (MPD + Access)

1. Créez toutes les tables avec les types appropriés
2. Définissez les relations avec intégrité référentielle
3. Ajoutez les masques de saisie et validations

### Étape 4 : Données de Test

Saisissez :
- 5 professeurs
- 10 élèves
- 5 instruments
- 8 cours
- 15 inscriptions

### Étape 5 : Requêtes Utiles

Créez les requêtes suivantes :
1. Liste des élèves par instrument
2. Planning d'un professeur (paramétré)
3. Élèves n'ayant pas de cours le mercredi
4. Nombre d'élèves par instrument
5. Chiffre d'affaires par professeur

---

## Exercice 11 : Auto-Évaluation

### Checklist de Compétences

Évaluez-vous de 1 à 5 :

| Compétence | Score |
|------------|-------|
| Créer une relation 1:N dans Access | /5 |
| Créer une relation N:M dans Access | /5 |
| Configurer l'intégrité référentielle | /5 |
| Créer une requête de sélection simple | /5 |
| Utiliser des critères dans les requêtes | /5 |
| Créer une requête multi-tables | /5 |
| Créer une requête paramétrée | /5 |
| Utiliser des champs calculés | /5 |
| Utiliser les fonctions d'agrégation | /5 |
| Écrire une requête en mode SQL | /5 |

### Points à Améliorer
Listez 3 points que vous souhaitez approfondir :
1. ____________________
2. ____________________
3. ____________________

---

## Ressources Aide-Mémoire

### Opérateurs SQL

| Opérateur | Usage |
|-----------|-------|
| SELECT | Sélection de colonnes |
| FROM | Source des données |
| WHERE | Condition de filtrage |
| ORDER BY | Tri des résultats |
| GROUP BY | Regroupement |
| HAVING | Condition sur les groupes |
| INNER JOIN | Jointure interne |
| LEFT JOIN | Jointure externe gauche |

### Fonctions Courantes

| Fonction | Description | Exemple |
|----------|-------------|---------|
| COUNT() | Comptage | COUNT(*) |
| SUM() | Somme | SUM(Montant) |
| AVG() | Moyenne | AVG(Prix) |
| MIN() | Minimum | MIN(Date) |
| MAX() | Maximum | MAX(Prix) |
| Date() | Date du jour | Date() |
| Year() | Année | Year([Date]) |
| IIf() | Condition | IIf(x>0,"Oui","Non") |

### Caractères Joker Access

| Caractère | Signification |
|-----------|---------------|
| * | Plusieurs caractères |
| ? | Un seul caractère |
| # | Un chiffre |
| [abc] | Un caractère parmi |
| [!abc] | Un caractère sauf |
