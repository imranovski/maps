# Corrigés Jour 5 - MS Access Avancé

## Exercice 1 : Création de Relations

### Configuration des Relations

**Relation Client → Commande**
```
Table principale : tblClient (NumClient)
Table liée : tblCommande (NumClient)
Type : Un à plusieurs (1:N)
☑ Appliquer l'intégrité référentielle
☑ Mettre à jour en cascade les champs correspondants
☐ Effacer en cascade les enregistrements correspondants
```

**Pourquoi ne pas activer la suppression en cascade ?**
- Risque de perte de données importantes (historique des commandes)
- Les commandes peuvent avoir une valeur comptable/légale
- Préférer une désactivation logique (champ Actif = Non)

**Relation Categorie → Produit**
```
Table principale : tblCategorie (CodeCategorie)
Table liée : tblProduit (CodeCategorie)
Type : Un à plusieurs (1:N)
☑ Appliquer l'intégrité référentielle
☑ Mettre à jour en cascade
☐ Effacer en cascade
```

**Relation Commande → LigneCommande**
```
Table principale : tblCommande (NumCommande)
Table liée : tblLigneCommande (NumCommande)
Type : Un à plusieurs (1:N)
☑ Appliquer l'intégrité référentielle
☑ Mettre à jour en cascade
☑ Effacer en cascade (acceptable ici : les lignes n'ont pas de sens sans commande)
```

### Relation N:M Produit-Fournisseur

**Table tblFournisseur** :
```
CodeFournisseur (PK) | Texte(10)
RaisonSociale        | Texte(100)
Adresse              | Texte(200)
Telephone            | Texte(14)
```

**Table tblFournit** :
```
CodeFournisseur (PK, FK) | Texte(10)
RefProduit (PK, FK)      | Texte(10)
PrixAchat                | Monétaire
DelaiLivraison           | Entier (jours)
```

---

## Exercice 2 : Requêtes de Sélection

### 1. qryListeProduits
```sql
SELECT p.RefProduit, p.Designation, p.PrixUnitaire, c.LibelleCategorie
FROM tblProduit AS p
INNER JOIN tblCategorie AS c ON p.CodeCategorie = c.CodeCategorie
ORDER BY p.Designation;
```

### 2. qryProduitsEnStock
```sql
SELECT RefProduit, Designation, QuantiteStock
FROM tblProduit
WHERE QuantiteStock > 0
ORDER BY QuantiteStock DESC;
```

### 3. qryProduitsAlerte
```sql
SELECT RefProduit, Designation, QuantiteStock, SeuilAlerte
FROM tblProduit
WHERE QuantiteStock < SeuilAlerte;
```

### 4. qryClientsParVille
```sql
SELECT Ville, COUNT(*) AS NbClients
FROM tblClient
GROUP BY Ville
ORDER BY COUNT(*) DESC;
```

### 5. qryCommandesRecentes
```sql
SELECT NumCommande, DateCommande, NumClient, MontantHT
FROM tblCommande
WHERE DateCommande >= DateAdd("d", -30, Date())
ORDER BY DateCommande DESC;
```

---

## Exercice 3 : Requêtes avec Critères

### 1. Produits dont le prix > 50€
```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
WHERE PrixUnitaire > 50;
```

### 2. Clients de Paris ou Lyon
```sql
SELECT NumClient, NomClient, Ville
FROM tblClient
WHERE Ville IN ('Paris', 'Lyon');

-- Alternative :
WHERE Ville = 'Paris' OR Ville = 'Lyon';
```

### 3. Commandes du mois en cours
```sql
SELECT NumCommande, DateCommande, NumClient
FROM tblCommande
WHERE Month(DateCommande) = Month(Date())
  AND Year(DateCommande) = Year(Date());

-- Alternative plus simple :
WHERE DateCommande >= DateSerial(Year(Date()), Month(Date()), 1);
```

### 4. Produits commençant par "A" et prix entre 10 et 100€
```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
WHERE Designation LIKE 'A*'
  AND PrixUnitaire BETWEEN 10 AND 100;
```

### 5. Clients ayant passé au moins une commande
```sql
SELECT DISTINCT c.NumClient, c.NomClient
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient;

-- Alternative avec sous-requête :
SELECT NumClient, NomClient
FROM tblClient
WHERE NumClient IN (SELECT NumClient FROM tblCommande);
```

### 6. Produits jamais commandés
```sql
SELECT p.RefProduit, p.Designation
FROM tblProduit AS p
LEFT JOIN tblLigneCommande AS lc ON p.RefProduit = lc.RefProduit
WHERE lc.RefProduit IS NULL;

-- Alternative :
SELECT RefProduit, Designation
FROM tblProduit
WHERE RefProduit NOT IN (SELECT RefProduit FROM tblLigneCommande);
```

---

## Exercice 4 : Requêtes Multi-Tables

### 2. Lignes de commande avec désignation produit
```sql
SELECT lc.NumCommande, lc.RefProduit, p.Designation, lc.Quantite, lc.PrixUnitaire
FROM tblLigneCommande AS lc
INNER JOIN tblProduit AS p ON lc.RefProduit = p.RefProduit;
```

### 3. Commandes avec détail complet
```sql
SELECT c.NomClient, cmd.NumCommande, cmd.DateCommande,
       p.Designation, lc.Quantite, lc.PrixUnitaire,
       lc.Quantite * lc.PrixUnitaire AS MontantLigne
FROM ((tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient)
INNER JOIN tblLigneCommande AS lc ON cmd.NumCommande = lc.NumCommande)
INNER JOIN tblProduit AS p ON lc.RefProduit = p.RefProduit
ORDER BY cmd.NumCommande, p.Designation;
```

### 4. Produits avec nom de catégorie
```sql
SELECT p.RefProduit, p.Designation, p.PrixUnitaire, c.LibelleCategorie
FROM tblProduit AS p
INNER JOIN tblCategorie AS c ON p.CodeCategorie = c.CodeCategorie;
```

### 5. Clients avec ou sans commandes
```sql
SELECT c.NumClient, c.NomClient, cmd.NumCommande, cmd.DateCommande
FROM tblClient AS c
LEFT JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
ORDER BY c.NomClient;
```

### 6. Produits avec ou sans ventes
```sql
SELECT p.RefProduit, p.Designation, SUM(lc.Quantite) AS TotalVendu
FROM tblProduit AS p
LEFT JOIN tblLigneCommande AS lc ON p.RefProduit = lc.RefProduit
GROUP BY p.RefProduit, p.Designation;
```

---

## Exercice 5 : Requêtes Paramétrées

### 1. qryCommandesClient
```sql
SELECT c.NomClient, cmd.NumCommande, cmd.DateCommande, cmd.MontantHT
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
WHERE c.NomClient LIKE '*' & [Entrez le nom du client] & '*'
ORDER BY cmd.DateCommande DESC;
```

### 2. qryCommandesPeriode
```sql
SELECT NumCommande, DateCommande, NumClient, MontantHT
FROM tblCommande
WHERE DateCommande BETWEEN [Date début] AND [Date fin]
ORDER BY DateCommande;
```

### 3. qryProduitsCategorie
```sql
SELECT p.RefProduit, p.Designation, p.PrixUnitaire, c.LibelleCategorie
FROM tblProduit AS p
INNER JOIN tblCategorie AS c ON p.CodeCategorie = c.CodeCategorie
WHERE c.LibelleCategorie = [Choisissez une catégorie];
```

### 4. qryProduitsRecherche
```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
WHERE Designation LIKE '*' & [Rechercher] & '*';
```

---

## Exercice 6 : Champs Calculés

### 1. Montant ligne
```
MontantLigne: [Quantite]*[PrixUnitaire]
```

### 2. Montant TTC
```
MontantTTC: [MontantHT]*(1+[TauxTVA])
```

### 3. Nom complet
```
NomComplet: [Prenom] & " " & [Nom]
```

### 4. Âge
```
Age: DateDiff("yyyy",[DateNaissance],Date())
```

Ou plus précis :
```
Age: DateDiff("yyyy",[DateNaissance],Date()) - IIf(Format(Date(),"mmdd") < Format([DateNaissance],"mmdd"), 1, 0)
```

### 5. Statut stock
```
StatutStock: IIf([QuantiteStock]<[SeuilAlerte],"ALERTE","OK")
```

### 6. Ancienneté client
```
Anciennete: DateDiff("yyyy",[DateInscription],Date())
```

---

## Exercice 7 : Fonctions d'Agrégation

### 1. Nombre total de produits
```sql
SELECT COUNT(*) AS NbProduits
FROM tblProduit;
```

### 2. Nombre de produits par catégorie
```sql
SELECT c.LibelleCategorie, COUNT(p.RefProduit) AS NbProduits
FROM tblCategorie AS c
LEFT JOIN tblProduit AS p ON c.CodeCategorie = p.CodeCategorie
GROUP BY c.LibelleCategorie
ORDER BY COUNT(p.RefProduit) DESC;
```

### 3. Chiffre d'affaires total
```sql
SELECT SUM(MontantHT) AS CATotal
FROM tblCommande
WHERE Statut <> 'Annulé';
```

### 4. CA par client
```sql
SELECT c.NomClient, SUM(cmd.MontantHT) AS CAClient
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
WHERE cmd.Statut <> 'Annulé'
GROUP BY c.NomClient
ORDER BY SUM(cmd.MontantHT) DESC;
```

### 5. Prix moyen par catégorie
```sql
SELECT c.LibelleCategorie, AVG(p.PrixUnitaire) AS PrixMoyen
FROM tblCategorie AS c
INNER JOIN tblProduit AS p ON c.CodeCategorie = p.CodeCategorie
GROUP BY c.LibelleCategorie;
```

### 6. Clients ayant commandé plus de 5 fois
```sql
SELECT c.NomClient, COUNT(cmd.NumCommande) AS NbCommandes
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
GROUP BY c.NomClient
HAVING COUNT(cmd.NumCommande) > 5
ORDER BY COUNT(cmd.NumCommande) DESC;
```

---

## Exercice 8 : Requêtes Action

### 2. Mise à jour statut commandes anciennes
```sql
UPDATE tblCommande
SET Statut = 'Archivé'
WHERE DateCommande < DateAdd("yyyy", -1, Date())
  AND Statut <> 'Annulé';
```

### 4. Suppression clients inactifs

**D'abord, vérifier avec SELECT** :
```sql
SELECT c.NumClient, c.NomClient, MAX(cmd.DateCommande) AS DerniereCommande
FROM tblClient AS c
LEFT JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
GROUP BY c.NumClient, c.NomClient
HAVING MAX(cmd.DateCommande) < DateAdd("yyyy", -2, Date())
   OR MAX(cmd.DateCommande) IS NULL;
```

**Ensuite, supprimer** :
```sql
DELETE FROM tblClient
WHERE NumClient IN (
    SELECT c.NumClient
    FROM tblClient AS c
    LEFT JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
    GROUP BY c.NumClient
    HAVING MAX(cmd.DateCommande) < DateAdd("yyyy", -2, Date())
       OR MAX(cmd.DateCommande) IS NULL
);
```

⚠️ **Attention** : Vérifier l'intégrité référentielle avant de supprimer !

---

## Exercice 9 : Mode SQL

### 2. Jointure avec alias
```sql
SELECT c.NomClient,
       cmd.NumCommande,
       cmd.DateCommande,
       SUM(lc.Quantite * lc.PrixUnitaire) AS TotalCommande
FROM tblClient AS c
INNER JOIN tblCommande AS cmd ON c.NumClient = cmd.NumClient
INNER JOIN tblLigneCommande AS lc ON cmd.NumCommande = lc.NumCommande
GROUP BY c.NomClient, cmd.NumCommande, cmd.DateCommande
ORDER BY cmd.DateCommande DESC;
```

### 3. Sous-requête (produits au-dessus de la moyenne)
```sql
SELECT RefProduit, Designation, PrixUnitaire
FROM tblProduit
WHERE PrixUnitaire > (SELECT AVG(PrixUnitaire) FROM tblProduit)
ORDER BY PrixUnitaire DESC;
```

### 4. Union clients et fournisseurs
```sql
SELECT NomClient AS Nom, Telephone, Email, 'Client' AS Type
FROM tblClient
UNION
SELECT RaisonSociale AS Nom, Telephone, Email, 'Fournisseur' AS Type
FROM tblFournisseur
ORDER BY Nom;
```

---

## Exercice 10 : Projet École de Musique

### MLD Complet
```
INSTRUMENT (CodeInstrument, LibelleInstrument, Famille)
            └─ PK ─────────┘

PROFESSEUR (NumProf, Nom, Prenom, Specialite, Telephone)
            └ PK ─┘

ELEVE (NumEleve, Nom, Prenom, DateNaissance, Adresse, Telephone, Email)
       └ PK ──┘

COURS (NumCours, Jour, Heure, Salle, Duree, #NumProf, #CodeInstrument)
       └ PK ──┘                            └ FK ───┘ └──── FK ───────┘

INSCRIPTION (#NumEleve, #NumCours, DateInscription, Niveau, TarifMensuel)
             └────── PK ────────┘
```

### Requêtes

**1. Liste des élèves par instrument**
```sql
SELECT i.LibelleInstrument, e.Nom, e.Prenom
FROM ((tblInstrument AS i
INNER JOIN tblCours AS c ON i.CodeInstrument = c.CodeInstrument)
INNER JOIN tblInscription AS insc ON c.NumCours = insc.NumCours)
INNER JOIN tblEleve AS e ON insc.NumEleve = e.NumEleve
ORDER BY i.LibelleInstrument, e.Nom;
```

**2. Planning d'un professeur (paramétré)**
```sql
SELECT p.Nom & ' ' & p.Prenom AS Professeur,
       c.Jour, c.Heure, c.Salle, c.Duree,
       i.LibelleInstrument
FROM (tblProfesseur AS p
INNER JOIN tblCours AS c ON p.NumProf = c.NumProf)
INNER JOIN tblInstrument AS i ON c.CodeInstrument = i.CodeInstrument
WHERE p.Nom = [Entrez le nom du professeur]
ORDER BY c.Jour, c.Heure;
```

**3. Élèves sans cours le mercredi**
```sql
SELECT e.NumEleve, e.Nom, e.Prenom
FROM tblEleve AS e
WHERE e.NumEleve NOT IN (
    SELECT insc.NumEleve
    FROM tblInscription AS insc
    INNER JOIN tblCours AS c ON insc.NumCours = c.NumCours
    WHERE c.Jour = 'Mercredi'
);
```

**4. Nombre d'élèves par instrument**
```sql
SELECT i.LibelleInstrument, COUNT(DISTINCT insc.NumEleve) AS NbEleves
FROM (tblInstrument AS i
INNER JOIN tblCours AS c ON i.CodeInstrument = c.CodeInstrument)
INNER JOIN tblInscription AS insc ON c.NumCours = insc.NumCours
GROUP BY i.LibelleInstrument
ORDER BY COUNT(DISTINCT insc.NumEleve) DESC;
```

**5. Chiffre d'affaires par professeur**
```sql
SELECT p.Nom & ' ' & p.Prenom AS Professeur,
       SUM(insc.TarifMensuel) AS CAMensuel
FROM ((tblProfesseur AS p
INNER JOIN tblCours AS c ON p.NumProf = c.NumProf)
INNER JOIN tblInscription AS insc ON c.NumCours = insc.NumCours)
GROUP BY p.Nom, p.Prenom
ORDER BY SUM(insc.TarifMensuel) DESC;
```
