# FICHE DE DÉROULEMENT - JOUR 5
## Maîtrise de MS Access et Projet Final

---

## 📋 INFORMATIONS DE LA SÉANCE

| Élément | Description |
|---------|-------------|
| **Jour** | Jour 5 sur 5 |
| **Durée** | 6 heures |
| **Thème** | Maîtrise de MS Access et Projet Final |
| **Public** | Professeurs d'Économie et Gestion |
| **Niveau** | Intermédiaire |

---

## 🎯 OBJECTIFS PÉDAGOGIQUES

À la fin de cette journée, les participants seront capables de :

1. Créer et gérer les relations entre tables
2. Assurer l'intégrité référentielle
3. Créer différents types de requêtes
4. Utiliser le mode SQL de base
5. Réaliser un projet complet intégrant Merise et Access
6. Appliquer les compétences acquises dans un contexte pédagogique

---

## 🛠️ MATÉRIEL ET RESSOURCES

### Matériel formateur
- [ ] Vidéoprojecteur
- [ ] Ordinateur avec MS Access installé
- [ ] Tableau blanc et marqueurs
- [ ] Supports de cours imprimés
- [ ] Certificats/Attestations

### Matériel participant
- [ ] Ordinateur avec MS Access installé
- [ ] Base de données GestionEcole créée au Jour 4
- [ ] Cahier de notes
- [ ] Support de cours Jour 5
- [ ] Questionnaire d'évaluation

### Documents à distribuer
- [ ] Polycopié "Relations et Requêtes Access"
- [ ] Fiche "Aide-mémoire SQL"
- [ ] Exercices Jour 5
- [ ] Énoncé du projet final

---

## ⏰ DÉROULEMENT DÉTAILLÉ

### MATINÉE (9h00 - 12h00)

---

### 🕘 SÉQUENCE 1 : Révision Jour 4 (9h00 - 9h15)

**Durée :** 15 minutes

**Objectif :** Consolider les acquis sur les tables Access

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Rappel création tables | Exposé | Diaporama |
| 5 min | Vérification des TP | Participatif | Access |
| 5 min | Questions/Réponses | Participatif | - |

#### Points de révision
- Modes de création de tables
- Types de données
- Propriétés des champs
- Import/Export

---

### 🕘 SÉQUENCE 2 : MS Access - Relations (9h15 - 11h00)

**Durée :** 1h45

**Objectif :** Maîtriser la création et gestion des relations

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 25 min | Création de relations | Démonstration + TP | Access |
| 25 min | Types de relations | Exposé + TP | Access |
| 25 min | Intégrité référentielle | Démonstration + TP | Access |
| 20 min | Propagation cascades | Démonstration + TP | Access |
| 10 min | Exercices pratiques | TP | Access |

#### Contenu détaillé

##### A. Fenêtre Relations

**Accès :**
1. Onglet **Outils de base de données** → **Relations**
2. La fenêtre Relations s'ouvre

**Interface :**
```
┌─────────────────────────────────────────────────────────┐
│ Outils de relation                                      │
│ ┌─────────────────────────────────────────────────────┐ │
│ │                                                     │ │
│ │  ┌───────────┐              ┌───────────┐          │ │
│ │  │  CLASSE   │              │ ETUDIANT  │          │ │
│ │  ├───────────┤              ├───────────┤          │ │
│ │  │CodeClasse │──────────────│NumEtudiant│          │ │
│ │  │Libelle    │      ∞       │Nom        │          │ │
│ │  │Niveau     │    1         │Prenom     │          │ │
│ │  └───────────┘              │DateNaiss  │          │ │
│ │                             │CodeClasse │          │ │
│ │                             └───────────┘          │ │
│ └─────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
```

##### B. Ajouter des tables à la fenêtre Relations

**Étapes :**
1. Clic droit dans la fenêtre → **Afficher la table**
2. OU Onglet **Création** → **Afficher la table**
3. Sélectionner les tables à ajouter
4. Cliquer sur **Ajouter**
5. Fermer la boîte de dialogue

##### C. Créer une relation

**Méthode par glisser-déposer :**
1. Identifier la clé primaire (côté 1)
2. Identifier la clé étrangère (côté N)
3. Glisser la clé primaire vers la clé étrangère
4. La boîte de dialogue **Modifier les relations** s'ouvre

**Boîte de dialogue Modifier les relations :**
```
┌──────────────────────────────────────────────────┐
│ Modifier les relations                            │
├──────────────────────────────────────────────────┤
│                                                  │
│  Table/Requête:        Table/Requête associée:   │
│  ┌────────────┐        ┌────────────┐            │
│  │  CLASSE    │        │  ETUDIANT  │            │
│  └────────────┘        └────────────┘            │
│                                                  │
│  CodeClasse      <-->  CodeClasse                │
│                                                  │
│  ☑ Appliquer l'intégrité référentielle          │
│  ☑ Mettre à jour en cascade les champs          │
│  ☑ Effacer en cascade les enregistrements       │
│                                                  │
│  Type de relation: Un-à-plusieurs               │
│                                                  │
│  [ Créer ]  [ Annuler ]  [ Type jointure ]      │
└──────────────────────────────────────────────────┘
```

##### D. Types de relations dans Access

###### Relation Un-à-Plusieurs (1:N)
- La plus courante
- Ex: Une CLASSE a plusieurs ETUDIANTS

###### Relation Un-à-Un (1:1)
- Moins fréquente
- Ex: Un EMPLOYE a un DOSSIER_MEDICAL

###### Relation Plusieurs-à-Plusieurs (N:N)
- Nécessite une table intermédiaire
- Ex: ETUDIANT - INSCRIPTION - COURS

**Implémentation N:N :**
```
┌───────────┐       ┌─────────────┐       ┌───────────┐
│ ETUDIANT  │       │ INSCRIPTION │       │   COURS   │
├───────────┤   1 ∞ ├─────────────┤ ∞ 1   ├───────────┤
│NumEtudiant│───────│NumEtudiant  │───────│CodeCours  │
│Nom        │       │CodeCours    │       │Intitule   │
│Prenom     │       │DateInsc     │       │NbHeures   │
└───────────┘       │Note         │       └───────────┘
                    └─────────────┘
```

##### E. Intégrité référentielle

**Définition :** Garantit la cohérence des données entre tables liées.

**Règles :**
1. Impossible d'ajouter un enregistrement avec une clé étrangère inexistante
2. Impossible de supprimer un enregistrement référencé par une autre table
3. Impossible de modifier une clé primaire référencée

**Activation :**
- Cocher **"Appliquer l'intégrité référentielle"** dans la boîte de dialogue

##### F. Propagation en cascade

###### Mise à jour en cascade
- Si la clé primaire change, la clé étrangère est automatiquement mise à jour
- Cocher **"Mettre à jour en cascade les champs correspondants"**

###### Suppression en cascade
- Si un enregistrement est supprimé, les enregistrements liés sont aussi supprimés
- Cocher **"Effacer en cascade les enregistrements correspondants"**
- ⚠️ **Attention** : utiliser avec précaution !

**Exemple :**
- Si on supprime une CLASSE avec cascade : tous les ETUDIANTS de cette classe sont supprimés
- Sans cascade : impossible de supprimer une CLASSE qui a des étudiants

##### G. Exercice pratique : Création de relations

**Dans la base GestionEcole.accdb :**

1. Créer la table MATIERE si pas fait :
   | Champ | Type | Clé |
   |-------|------|-----|
   | CodeMatiere | Texte court (5) | PK |
   | Libelle | Texte court (50) | |
   | Coefficient | Numérique | |

2. Créer la table NOTE (table intermédiaire) :
   | Champ | Type | Clé |
   |-------|------|-----|
   | NumEtudiant | Numérique (Entier long) | PK, FK |
   | CodeMatiere | Texte court (5) | PK, FK |
   | DateEval | Date/Heure | PK |
   | Valeur | Numérique (Réel simple) | |
   | TypeEval | Texte court (20) | |

3. Ajouter CodeClasse à la table ETUDIANT si pas fait

4. Créer les relations :
   - CLASSE → ETUDIANT (1:N)
   - ETUDIANT → NOTE (1:N)
   - MATIERE → NOTE (1:N)

5. Activer l'intégrité référentielle pour chaque relation

---

### ☕ PAUSE CAFÉ (11h00 - 11h15)

---

### 🕚 SÉQUENCE 3 : MS Access - Requêtes Partie 1 (11h15 - 12h00)

**Durée :** 45 minutes

**Objectif :** Créer des requêtes de sélection simples

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 10 min | Introduction aux requêtes | Exposé | Diaporama |
| 15 min | Requêtes avec l'assistant | Démonstration + TP | Access |
| 20 min | Mode Création (QBE) | Démonstration + TP | Access |

#### Contenu détaillé

##### A. Qu'est-ce qu'une requête ?

**Définition :** Outil permettant d'interroger la base de données pour extraire, filtrer, trier ou manipuler les données.

**Types de requêtes :**
| Type | Fonction |
|------|----------|
| **Sélection** | Extraire des données (SELECT) |
| **Ajout** | Ajouter des enregistrements (INSERT) |
| **Mise à jour** | Modifier des données (UPDATE) |
| **Suppression** | Supprimer des enregistrements (DELETE) |
| **Création table** | Créer une nouvelle table |
| **Analyse croisée** | Tableaux croisés dynamiques |

##### B. L'Assistant Requête

**Accès :** Onglet **Créer** → **Assistant Requête**

**Étapes :**
1. Choisir le type d'assistant
2. Sélectionner les tables/requêtes
3. Choisir les champs
4. Définir le tri
5. Nommer la requête

##### C. Mode Création (Query By Example - QBE)

**Accès :** Onglet **Créer** → **Création de requête**

**Interface QBE :**
```
┌─────────────────────────────────────────────────────────┐
│ Tables disponibles                                       │
│ ┌───────────┐  ┌───────────┐  ┌───────────┐             │
│ │ ETUDIANT  │  │  CLASSE   │  │  MATIERE  │             │
│ └───────────┘  └───────────┘  └───────────┘             │
├─────────────────────────────────────────────────────────┤
│ Grille de requête                                        │
│ ┌─────────┬─────────┬─────────┬─────────┬─────────┐     │
│ │ Champ   │ Nom     │ Prenom  │ Libelle │         │     │
│ │ Table   │ ETUDIANT│ ETUDIANT│ CLASSE  │         │     │
│ │ Tri     │ Croiss. │         │         │         │     │
│ │ Afficher│   ☑     │   ☑     │   ☑     │         │     │
│ │ Critères│         │         │ ="BTS1" │         │     │
│ │ Ou      │         │         │         │         │     │
│ └─────────┴─────────┴─────────┴─────────┴─────────┘     │
└─────────────────────────────────────────────────────────┘
```

**Éléments de la grille :**
| Ligne | Fonction |
|-------|----------|
| **Champ** | Nom du champ à afficher/utiliser |
| **Table** | Table d'origine du champ |
| **Tri** | Tri croissant/décroissant |
| **Afficher** | Afficher le champ dans le résultat |
| **Critères** | Condition de filtrage |
| **Ou** | Critère alternatif (OU logique) |

##### D. Exercice pratique : Requêtes simples

**Requête 1 :** Liste de tous les étudiants
- Champs : NumEtudiant, Nom, Prenom
- Tri : Nom croissant

**Requête 2 :** Liste des étudiants d'une classe
- Champs : Nom, Prenom, Libelle (classe)
- Critère : Libelle = "BTS1"

**Requête 3 :** Étudiants nés après 2000
- Champs : Nom, Prenom, DateNaissance
- Critère : DateNaissance > #01/01/2000#

---

### 🍽️ PAUSE DÉJEUNER (12h00 - 13h30)

---

### APRÈS-MIDI (13h30 - 16h30)

---

### 🕜 SÉQUENCE 4 : MS Access - Requêtes Partie 2 (13h30 - 14h30)

**Durée :** 1 heure

**Objectif :** Maîtriser les requêtes avancées

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 15 min | Critères et opérateurs | Exposé + TP | Access |
| 15 min | Requêtes multi-tables | Démonstration + TP | Access |
| 15 min | Requêtes paramétrées | Démonstration + TP | Access |
| 15 min | Champs calculés | Démonstration + TP | Access |

#### Contenu détaillé

##### A. Critères de sélection

###### Opérateurs de comparaison
| Opérateur | Signification | Exemple |
|-----------|---------------|---------|
| `=` | Égal | `="Paris"` |
| `<>` | Différent | `<>"Paris"` |
| `<` | Inférieur | `<100` |
| `<=` | Inférieur ou égal | `<=100` |
| `>` | Supérieur | `>100` |
| `>=` | Supérieur ou égal | `>=100` |
| `Between` | Entre deux valeurs | `Between 10 And 20` |
| `In` | Dans une liste | `In("Paris";"Lyon";"Marseille")` |
| `Like` | Correspondance partielle | `Like "D*"` |
| `Is Null` | Valeur nulle | `Is Null` |
| `Is Not Null` | Valeur non nulle | `Is Not Null` |

###### Opérateurs logiques
| Opérateur | Signification |
|-----------|---------------|
| `And` | ET logique (même ligne) |
| `Or` | OU logique (lignes différentes) |
| `Not` | Négation |

###### Caractères génériques (avec Like)
| Caractère | Signification | Exemple |
|-----------|---------------|---------|
| `*` | N'importe quels caractères | `Like "D*"` → Dupont, Durand |
| `?` | Un caractère quelconque | `Like "?upont"` → Dupont, Tupont |
| `#` | Un chiffre | `Like "75###"` → codes postaux Paris |
| `[abc]` | Un caractère parmi | `Like "[DM]*"` → commence par D ou M |
| `[!abc]` | Sauf ces caractères | `Like "[!DM]*"` → ne commence pas par D ni M |

##### B. Requêtes multi-tables (Jointures)

**Principe :** Combiner des données de plusieurs tables liées.

**Types de jointures :**
| Type | Description | Inclut |
|------|-------------|--------|
| **Interne** (défaut) | Enregistrements correspondants | Uniquement les lignes liées |
| **Externe gauche** | Tous les enregistrements de gauche | Tous côté 1, même sans correspondance |
| **Externe droite** | Tous les enregistrements de droite | Tous côté N, même sans correspondance |

**Exemple :**
```
Requête: Étudiants avec leur classe
Tables: ETUDIANT et CLASSE (liées par CodeClasse)
Champs: ETUDIANT.Nom, ETUDIANT.Prenom, CLASSE.Libelle
```

##### C. Requêtes paramétrées

**Définition :** Requête qui demande une valeur à l'utilisateur au moment de l'exécution.

**Syntaxe :** `[Texte de l'invite]`

**Exemple :**
```
Critère du champ Libelle: [Entrez le nom de la classe:]
```

À l'exécution, une boîte de dialogue s'affiche pour saisir la valeur.

##### D. Champs calculés

**Syntaxe :** `NomChamp: Expression`

**Exemples :**
| Expression | Résultat |
|------------|----------|
| `NomComplet: [Nom] & " " & [Prenom]` | DUPONT Marie |
| `PrixTTC: [PrixHT] * 1.2` | Calcul TTC |
| `Age: DateDiff("yyyy";[DateNaissance];Date())` | Âge en années |
| `Remise: IIf([Quantite]>10;0.1;0)` | 10% si qté > 10 |

###### Fonctions utiles
| Fonction | Description | Exemple |
|----------|-------------|---------|
| `Date()` | Date du jour | `=Date()` |
| `Now()` | Date et heure actuelles | `=Now()` |
| `Year()` | Extraire l'année | `Year([DateNaissance])` |
| `Month()` | Extraire le mois | `Month([DateNaissance])` |
| `DateDiff()` | Différence entre dates | `DateDiff("yyyy";[Date1];[Date2])` |
| `IIf()` | Condition Si | `IIf([Note]>=10;"Admis";"Refusé")` |
| `UCase()` | Majuscules | `UCase([Nom])` |
| `Left()` | Premiers caractères | `Left([Nom];3)` |

---

### 🕜 SÉQUENCE 5 : MS Access - Requêtes Partie 3 (14h30 - 15h30)

**Durée :** 1 heure

**Objectif :** Maîtriser les requêtes action et le SQL

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 20 min | Requêtes Action | Démonstration + TP | Access |
| 20 min | Requêtes Analyse croisée | Démonstration + TP | Access |
| 20 min | Introduction au SQL | Exposé + Démonstration | Access |

#### Contenu détaillé

##### A. Requêtes Action

**⚠️ Attention :** Les requêtes action modifient les données de façon permanente !

###### Requête d'ajout (INSERT)
- Ajoute des enregistrements d'une table/requête vers une autre
- Onglet **Création** → **Ajout**

**Exemple :** Copier tous les étudiants de BTS1 vers une table ARCHIVES

###### Requête de mise à jour (UPDATE)
- Modifie les valeurs de champs existants
- Onglet **Création** → **Mise à jour**

**Exemple :** Augmenter tous les prix de 5%
```
Table: PRODUIT
Champ: PrixHT
Mise à jour: [PrixHT] * 1.05
```

###### Requête de suppression (DELETE)
- Supprime des enregistrements selon critères
- Onglet **Création** → **Suppression**

**Exemple :** Supprimer les étudiants inactifs depuis 2 ans

###### Requête de création de table
- Crée une nouvelle table à partir du résultat
- Onglet **Création** → **Création de table**

**Exemple :** Créer une table PALMARES avec les meilleurs étudiants

##### B. Requêtes Analyse croisée

**Définition :** Affiche les données sous forme de tableau croisé (lignes × colonnes).

**Exemple :** Moyenne des notes par matière et par classe
```
              │ Maths │ Français │ Anglais │
──────────────┼───────┼──────────┼─────────┤
BTS1          │ 12.5  │  14.2    │  13.1   │
BTS2          │ 11.8  │  13.5    │  14.0   │
```

**Création :**
1. Onglet **Créer** → **Assistant Requête** → **Analyse croisée**
2. Choisir la table/requête source
3. Définir les en-têtes de lignes
4. Définir les en-têtes de colonnes
5. Choisir la fonction d'agrégation (Somme, Moyenne, Compte...)

##### C. Introduction au SQL

**SQL = Structured Query Language**

###### Afficher le SQL d'une requête
1. Créer/ouvrir une requête en mode Création
2. Onglet **Création** → **Affichage** → **Mode SQL**

###### Syntaxe de base SELECT
```sql
SELECT champ1, champ2, ...
FROM table
WHERE condition
ORDER BY champ [ASC|DESC];
```

**Exemples :**

```sql
-- Liste de tous les étudiants
SELECT Nom, Prenom
FROM ETUDIANT;

-- Étudiants de BTS1
SELECT E.Nom, E.Prenom, C.Libelle
FROM ETUDIANT AS E
INNER JOIN CLASSE AS C ON E.CodeClasse = C.CodeClasse
WHERE C.Libelle = 'BTS1';

-- Nombre d'étudiants par classe
SELECT C.Libelle, COUNT(*) AS NbEtudiants
FROM ETUDIANT AS E
INNER JOIN CLASSE AS C ON E.CodeClasse = C.CodeClasse
GROUP BY C.Libelle;

-- Moyenne des notes par étudiant
SELECT E.Nom, E.Prenom, AVG(N.Valeur) AS Moyenne
FROM ETUDIANT AS E
INNER JOIN NOTE AS N ON E.NumEtudiant = N.NumEtudiant
GROUP BY E.Nom, E.Prenom
HAVING AVG(N.Valeur) >= 10;
```

###### Clauses SQL principales
| Clause | Fonction |
|--------|----------|
| `SELECT` | Champs à afficher |
| `FROM` | Tables sources |
| `WHERE` | Conditions de filtrage |
| `ORDER BY` | Tri des résultats |
| `GROUP BY` | Regroupement pour agrégation |
| `HAVING` | Condition sur les groupes |
| `JOIN` | Jointure entre tables |

---

### ☕ PAUSE (15h30 - 15h45)

---

### 🕞 SÉQUENCE 6 : Projet Pratique Final (15h45 - 16h15)

**Durée :** 30 minutes

**Objectif :** Appliquer toutes les compétences acquises

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Présentation du projet | Exposé | Énoncé |
| 20 min | Travail en groupe | TP | Access |
| 5 min | Restitution rapide | Participatif | - |

---

#### 📝 PROJET FINAL : Application complète

**Contexte :**
Vous êtes enseignant et souhaitez créer une base de données pour gérer les évaluations de vos élèves.

**Objectif :** Concevoir et implémenter une base de données complète.

##### Partie 1 : Conception Merise (si temps disponible, sinon fournir le MCD)

**Cahier des charges :**
1. Gérer les élèves (numéro, nom, prénom, date naissance, email)
2. Gérer les classes (code, libellé, niveau)
3. Gérer les matières (code, libellé, coefficient)
4. Gérer les enseignants (numéro, nom, prénom, spécialité)
5. Un enseignant peut enseigner plusieurs matières
6. Un élève appartient à une classe
7. Gérer les notes (date, type évaluation, note sur 20)

**Travail demandé :**
- Dessiner le MCD
- Transformer en MLD

##### Partie 2 : Implémentation Access

**À créer :**
1. Les tables avec leurs champs et types
2. Les relations avec intégrité référentielle
3. Saisir quelques données de test

##### Partie 3 : Requêtes

**Requêtes à créer :**
1. Liste des élèves par classe (triée par nom)
2. Moyenne des notes par élève
3. Moyenne par matière
4. Élèves ayant une moyenne >= 12
5. Nombre d'élèves par classe

##### Solution MLD fournie

```
CLASSE (CodeClasse, Libelle, Niveau)

ETUDIANT (NumEtudiant, Nom, Prenom, DateNaissance, Email, #CodeClasse)

MATIERE (CodeMatiere, Libelle, Coefficient)

ENSEIGNANT (NumEnseignant, Nom, Prenom, Specialite)

ENSEIGNER (#NumEnseignant, #CodeMatiere)

NOTE (#NumEtudiant, #CodeMatiere, DateEval, TypeEval, Valeur)
```

---

### 🕟 SÉQUENCE 7 : Évaluation et Clôture (16h15 - 16h30)

**Durée :** 15 minutes

**Objectif :** Évaluer les acquis et clôturer la formation

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Bilan de la formation | Discussion | - |
| 5 min | Questionnaire de satisfaction | Individuel | Formulaire |
| 5 min | Remise des attestations | Cérémonie | Attestations |

#### Contenu

##### A. Bilan de la formation

**Questions de discussion :**
- Qu'avez-vous appris de plus utile ?
- Quels sujets nécessiteraient un approfondissement ?
- Comment comptez-vous utiliser ces connaissances ?

##### B. Évaluation des acquis

**QCM rapide (5 questions) :**

1. Quel niveau de Merise est indépendant du SGBD ?
   - [ ] MCD
   - [ ] MLD
   - [ ] MPD

2. Une relation 1:N dans le MCD devient dans le MLD :
   - [ ] Une table intermédiaire
   - [ ] Une clé étrangère côté N
   - [ ] Rien

3. Pour garantir la cohérence des données entre tables, on active :
   - [ ] La clé primaire
   - [ ] L'intégrité référentielle
   - [ ] Le mode création

4. Une requête paramétrée :
   - [ ] Modifie les données
   - [ ] Demande une valeur à l'utilisateur
   - [ ] Crée une nouvelle table

5. La clause SQL pour filtrer les résultats est :
   - [ ] SELECT
   - [ ] WHERE
   - [ ] ORDER BY

**Réponses :** 1-MLD, 2-Clé étrangère côté N, 3-Intégrité référentielle, 4-Demande une valeur, 5-WHERE

##### C. Questionnaire de satisfaction

| Critère | 1 | 2 | 3 | 4 | 5 |
|---------|---|---|---|---|---|
| Contenu de la formation | ☐ | ☐ | ☐ | ☐ | ☐ |
| Qualité pédagogique | ☐ | ☐ | ☐ | ☐ | ☐ |
| Supports fournis | ☐ | ☐ | ☐ | ☐ | ☐ |
| Travaux pratiques | ☐ | ☐ | ☐ | ☐ | ☐ |
| Applicabilité | ☐ | ☐ | ☐ | ☐ | ☐ |
| Organisation générale | ☐ | ☐ | ☐ | ☐ | ☐ |

**Commentaires libres :**

##### D. Perspectives d'utilisation pédagogique

**Applications possibles :**
- Créer des TD/TP pour les élèves
- Modéliser des cas d'entreprise
- Préparer aux examens (BTS, DCG)
- Réaliser des projets transversaux

**Ressources complémentaires :**
- Documentation Microsoft Access
- Tutoriels vidéo
- Forum d'entraide
- Exercices supplémentaires

##### E. Remise des attestations

Remise individuelle des attestations de formation avec :
- Nom du participant
- Intitulé de la formation
- Durée (30 heures)
- Compétences acquises
- Signature du formateur

---

## ✅ SYNTHÈSE FINALE DE LA FORMATION

### Compétences acquises

| Jour | Compétences |
|------|-------------|
| **Jour 1** | Merise, SGBD, Modèle E/A |
| **Jour 2** | MCT, MCD, Normalisation |
| **Jour 3** | MCD avancé, MLD, Transformation |
| **Jour 4** | MPD, Interface Access, Tables |
| **Jour 5** | Relations, Requêtes, SQL, Projet |

### Récapitulatif Merise

```
         RÉEL                 CONCEPTUEL              LOGIQUE               PHYSIQUE
    ┌───────────┐           ┌───────────┐          ┌───────────┐         ┌───────────┐
    │ Problème  │  ────►    │    MCD    │  ────►   │    MLD    │  ────►  │    MPD    │
    │ métier    │           │    MCT    │          │    MLT    │         │    MPT    │
    └───────────┘           └───────────┘          └───────────┘         └───────────┘
                                                                               │
                                                                               ▼
                                                                        ┌───────────┐
                                                                        │   BASE    │
                                                                        │  ACCESS   │
                                                                        └───────────┘
```

### Récapitulatif Access

| Objet | Utilisation |
|-------|-------------|
| **Tables** | Stockage structuré des données |
| **Relations** | Liens entre tables, intégrité |
| **Requêtes** | Interrogation et manipulation |
| **Formulaires** | Interfaces de saisie (non couvert) |
| **États** | Rapports imprimables (non couvert) |

---

## 📊 ÉVALUATION DE LA SÉANCE

### Grille d'observation formateur

| Critère | Non acquis | En cours | Acquis |
|---------|------------|----------|--------|
| Création de relations | ☐ | ☐ | ☐ |
| Intégrité référentielle | ☐ | ☐ | ☐ |
| Requêtes sélection | ☐ | ☐ | ☐ |
| Requêtes avec critères | ☐ | ☐ | ☐ |
| Requêtes multi-tables | ☐ | ☐ | ☐ |
| Compréhension SQL | ☐ | ☐ | ☐ |
| Projet global | ☐ | ☐ | ☐ |

### Auto-évaluation finale participant

**Je suis capable de :**

| Compétence | Oui | Partiellement | Non |
|------------|-----|---------------|-----|
| Modéliser un SI avec Merise | ☐ | ☐ | ☐ |
| Créer un MCD complet | ☐ | ☐ | ☐ |
| Transformer un MCD en MLD | ☐ | ☐ | ☐ |
| Créer des tables Access | ☐ | ☐ | ☐ |
| Définir des relations | ☐ | ☐ | ☐ |
| Créer des requêtes | ☐ | ☐ | ☐ |
| Utiliser SQL basique | ☐ | ☐ | ☐ |
| Appliquer à mon enseignement | ☐ | ☐ | ☐ |

---

## 📎 DOCUMENTS ANNEXES JOUR 5

- Annexe 5A : Diaporama "Relations et Requêtes Access"
- Annexe 5B : Fiche "Aide-mémoire SQL"
- Annexe 5C : Fiche "Opérateurs et fonctions Access"
- Annexe 5D : Exercices et corrigés Jour 5
- Annexe 5E : Énoncé du projet final
- Annexe 5F : Solution du projet final
- Annexe 5G : Questionnaire d'évaluation
- Annexe 5H : Modèle d'attestation
