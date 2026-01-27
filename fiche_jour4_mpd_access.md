# FICHE DE DÉROULEMENT - JOUR 4
## MPD et Introduction à MS Access

---

## 📋 INFORMATIONS DE LA SÉANCE

| Élément | Description |
|---------|-------------|
| **Jour** | Jour 4 sur 5 |
| **Durée** | 6 heures |
| **Thème** | MPD et Introduction à MS Access |
| **Public** | Professeurs d'Économie et Gestion |
| **Niveau** | Intermédiaire |

---

## 🎯 OBJECTIFS PÉDAGOGIQUES

À la fin de cette journée, les participants seront capables de :

1. Comprendre le Modèle Physique de Données (MPD)
2. Définir les types de données et contraintes
3. Naviguer dans l'interface MS Access
4. Créer une base de données Access
5. Créer et configurer des tables
6. Saisir et manipuler des données

---

## 🛠️ MATÉRIEL ET RESSOURCES

### Matériel formateur
- [ ] Vidéoprojecteur
- [ ] Ordinateur avec MS Access installé
- [ ] Tableau blanc et marqueurs
- [ ] Supports de cours imprimés

### Matériel participant
- [ ] Ordinateur avec MS Access installé
- [ ] Cahier de notes
- [ ] Support de cours Jour 4
- [ ] Fiches d'exercices
- [ ] MLD créé au Jour 3

### Documents à distribuer
- [ ] Polycopié "MPD et Access"
- [ ] Fiche "Types de données Access"
- [ ] Exercices Jour 4

---

## ⏰ DÉROULEMENT DÉTAILLÉ

### MATINÉE (9h00 - 12h00)

---

### 🕘 SÉQUENCE 1 : Révision Jour 3 (9h00 - 9h15)

**Durée :** 15 minutes

**Objectif :** Consolider les acquis sur le MLD

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 5 min | Rappel des règles de transformation | Exposé | Diaporama |
| 5 min | Vérification exercice maison | Participatif | Tableau |
| 5 min | Questions/Réponses | Participatif | - |

#### Points de révision
- Transformation entités → tables
- Transformation associations (1:N, N:N, 1:1)
- Gestion des clés primaires et étrangères

---

### 🕘 SÉQUENCE 2 : Modèle MPD (9h15 - 10h15)

**Durée :** 1 heure

**Objectif :** Comprendre le passage du MLD au MPD

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 15 min | Implémentation physique | Exposé | Diaporama |
| 15 min | Types de données | Exposé | Diaporama |
| 15 min | Contraintes et index | Exposé | Diaporama |
| 15 min | Exercices pratiques | Travail dirigé | Fiche |

#### Contenu détaillé

##### A. Introduction au MPD

**Définition :** Le MPD représente la structure de la base de données telle qu'elle sera implémentée dans un SGBD spécifique.

**Caractéristiques :**
- Dépendant du SGBD choisi
- Inclut les types de données spécifiques
- Définit les contraintes d'intégrité
- Optimise les performances (index)

**Position dans Merise :**
```
    MCD ──► MLD ──► MPD ──► BASE DE DONNÉES
                    ↑              ↓
               Indépendant    Dépendant du SGBD
               du SGBD        (Access, MySQL, etc.)
```

##### B. Types de données

###### Types de données génériques

| Type générique | Description | Exemples |
|----------------|-------------|----------|
| Entier | Nombres entiers | 1, 42, -100 |
| Réel | Nombres décimaux | 3.14, 99.99 |
| Caractère | Texte court | 'ABC' |
| Chaîne | Texte long | 'Bonjour monde' |
| Date | Date | 2024-01-15 |
| Booléen | Vrai/Faux | True, False |

###### Types de données MS Access

| Type Access | Description | Taille |
|-------------|-------------|--------|
| **Texte court** | Texte jusqu'à 255 car. | Variable |
| **Texte long** | Texte illimité | Variable |
| **Numérique** | Nombres | 1-16 octets |
| **Numéro automatique** | Incrémentation auto | 4 octets |
| **Date/Heure** | Dates et heures | 8 octets |
| **Monétaire** | Valeurs monétaires | 8 octets |
| **Oui/Non** | Valeur booléenne | 1 bit |
| **Pièce jointe** | Fichiers attachés | Variable |
| **Lien hypertexte** | URL | Variable |

##### C. Contraintes d'intégrité

| Contrainte | Description | Exemple |
|------------|-------------|---------|
| **NOT NULL** | Valeur obligatoire | Nom client obligatoire |
| **UNIQUE** | Valeur unique | Email unique |
| **PRIMARY KEY** | Clé primaire (unique + not null) | NumClient |
| **FOREIGN KEY** | Référence vers autre table | CodeDept dans EMPLOYE |
| **CHECK** | Condition à respecter | Age >= 0 |
| **DEFAULT** | Valeur par défaut | DateCreation = Aujourd'hui |

##### D. Les Index

**Définition :** Structure de données pour accélérer les recherches.

**Types :**
- **Index simple** : sur une colonne
- **Index composé** : sur plusieurs colonnes
- **Index unique** : garantit l'unicité

**Quand créer un index ?**
- Clés primaires (automatique)
- Clés étrangères
- Colonnes fréquemment utilisées dans WHERE
- Colonnes utilisées pour les jointures

##### E. Exercice pratique : MPD de la gestion commerciale

**MLD donné :**
```
CLIENT (NumClient, Nom, Prenom, Email, Tel)
PRODUIT (RefProd, Designation, PrixHT, QteStock, #CodeCat)
COMMANDE (NumCmd, DateCmd, #NumClient)
LIGNE_COMMANDE (#NumCmd, #RefProd, Quantite, PrixVente)
```

**Travail demandé :** Définir les types de données pour MS Access.

**Solution :**

| Table | Attribut | Type Access | Taille | Contraintes |
|-------|----------|-------------|--------|-------------|
| CLIENT | NumClient | NuméroAuto | - | PK |
| CLIENT | Nom | Texte court | 50 | NOT NULL |
| CLIENT | Prenom | Texte court | 50 | |
| CLIENT | Email | Texte court | 100 | UNIQUE |
| CLIENT | Tel | Texte court | 15 | |
| PRODUIT | RefProd | Texte court | 10 | PK |
| PRODUIT | Designation | Texte court | 100 | NOT NULL |
| PRODUIT | PrixHT | Monétaire | - | >= 0 |
| PRODUIT | QteStock | Numérique (Entier) | - | >= 0 |
| PRODUIT | CodeCat | Texte court | 5 | FK |
| COMMANDE | NumCmd | NuméroAuto | - | PK |
| COMMANDE | DateCmd | Date/Heure | - | NOT NULL |
| COMMANDE | NumClient | Numérique (Entier long) | - | FK, NOT NULL |
| LIGNE_COMMANDE | NumCmd | Numérique (Entier long) | - | PK, FK |
| LIGNE_COMMANDE | RefProd | Texte court | 10 | PK, FK |
| LIGNE_COMMANDE | Quantite | Numérique (Entier) | - | > 0 |
| LIGNE_COMMANDE | PrixVente | Monétaire | - | >= 0 |

---

### ☕ PAUSE CAFÉ (10h15 - 10h30)

---

### 🕥 SÉQUENCE 3 : MS Access - Introduction (10h30 - 12h00)

**Durée :** 1h30

**Objectif :** Découvrir l'interface MS Access et créer une base de données

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 30 min | Présentation de l'interface | Démonstration | Access |
| 30 min | Création d'une base de données | Travaux pratiques | Access |
| 30 min | Organisation et bonnes pratiques | Exposé + TP | Access |

#### Contenu détaillé

##### A. Présentation de l'interface

###### Lancement d'Access
1. Menu Démarrer → Microsoft Access
2. Page d'accueil avec options :
   - Nouvelle base de données vide
   - Modèles prédéfinis
   - Ouvrir une base existante

###### Éléments de l'interface

```
┌───────────────────────────────────────────────────────────────┐
│  Barre de titre                                          _ □ X │
├───────────────────────────────────────────────────────────────┤
│  Fichier │ Accueil │ Créer │ Données externes │ Outils BD    │ ← RUBAN
├───────────────────────────────────────────────────────────────┤
│          │                                                    │
│  Volet   │                                                    │
│  de      │           Zone de travail principale               │
│  navig.  │                                                    │
│          │                                                    │
│ ─────────│                                                    │
│ Tables   │                                                    │
│ Requêtes │                                                    │
│ Formulaires│                                                  │
│ États    │                                                    │
│          │                                                    │
├───────────────────────────────────────────────────────────────┤
│  Barre d'état                                                 │
└───────────────────────────────────────────────────────────────┘
```

###### Le Ruban - Onglets principaux

| Onglet | Fonctions |
|--------|-----------|
| **Fichier** | Nouveau, Ouvrir, Enregistrer, Imprimer |
| **Accueil** | Presse-papiers, Tri, Filtres |
| **Créer** | Tables, Requêtes, Formulaires, États |
| **Données externes** | Import/Export |
| **Outils de base de données** | Relations, Analyser, Macros |

###### Le Volet de navigation
- Affiche tous les objets de la base
- Organisation par type ou par groupe
- Clic droit pour les options

##### B. Les Objets Access

| Objet | Icône | Description |
|-------|-------|-------------|
| **Table** | 📋 | Stockage des données |
| **Requête** | 🔍 | Interrogation/manipulation des données |
| **Formulaire** | 📝 | Interface de saisie |
| **État** | 📄 | Impression/Rapport |
| **Macro** | ⚙️ | Automatisation |
| **Module** | 💻 | Code VBA |

##### C. Création d'une base de données

###### Étapes de création

1. **Fichier → Nouveau → Base de données vide**
2. **Nommer la base** : GestionCommerciale.accdb
3. **Choisir l'emplacement** : Documents\Formation
4. **Cliquer sur Créer**

###### Extension .accdb
- Format Access 2007 et versions ultérieures
- Remplacement de .mdb (Access 2003)
- Meilleures performances et sécurité

##### D. Organisation de la base de données

###### Bonnes pratiques
- Nommer les objets de façon explicite
- Utiliser des préfixes : tbl_Client, qry_VentesParMois
- Documenter les objets
- Faire des sauvegardes régulières

###### Convention de nommage suggérée

| Objet | Préfixe | Exemple |
|-------|---------|---------|
| Table | tbl_ | tbl_Client |
| Requête | qry_ | qry_ClientsActifs |
| Formulaire | frm_ | frm_SaisieClient |
| État | rpt_ | rpt_ListeClients |
| Macro | mcr_ | mcr_OuvrirFormulaire |

##### E. Sauvegarde et restauration

###### Sauvegarde
- Fichier → Enregistrer sous → Base de données
- Copier le fichier .accdb régulièrement
- Créer une archive datée

###### Restauration
- Copier la sauvegarde
- Renommer si nécessaire
- Ouvrir dans Access

---

#### 💻 TRAVAUX PRATIQUES - Création de la base

**Exercice guidé :**

1. Lancer MS Access
2. Créer une nouvelle base de données vide
3. La nommer : **GestionEcole.accdb**
4. L'enregistrer dans : **Documents\Formation**
5. Explorer l'interface
6. Fermer et rouvrir la base

---

### 🍽️ PAUSE DÉJEUNER (12h00 - 13h30)

---

### APRÈS-MIDI (13h30 - 16h30)

---

### 🕜 SÉQUENCE 4 : MS Access - Tables Partie 1 (13h30 - 14h45)

**Durée :** 1h15

**Objectif :** Créer et configurer des tables en mode Création

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 20 min | Création de tables en mode Création | Démonstration + TP | Access |
| 20 min | Définition des champs | Démonstration + TP | Access |
| 20 min | Propriétés des champs | Démonstration + TP | Access |
| 15 min | Clés primaires | Démonstration + TP | Access |

#### Contenu détaillé

##### A. Modes de création de tables

###### Mode Feuille de données
- Création rapide
- Saisie directe
- Types déduits automatiquement
- Moins de contrôle

###### Mode Création (recommandé)
- Contrôle total
- Définition précise des types
- Configuration des propriétés
- Meilleure qualité

##### B. Création en mode Création

**Accès :**
1. Onglet **Créer** → **Création de table**
2. Fenêtre de conception s'ouvre

**Interface mode Création :**
```
┌─────────────────────────────────────────────────────────┐
│ Nom du champ      │ Type de données │ Description       │
├───────────────────┼─────────────────┼───────────────────┤
│ NumEtudiant       │ NuméroAuto      │ ID automatique    │
│ Nom               │ Texte court     │ Nom de famille    │
│ Prenom            │ Texte court     │ Prénom            │
│ DateNaissance     │ Date/Heure      │ Date de naissance │
│ Email             │ Texte court     │ Adresse email     │
├───────────────────┴─────────────────┴───────────────────┤
│ Propriétés du champ                                      │
│ ┌─────────────────────────────────────────────────────┐ │
│ │ Général │ Liste de choix │                          │ │
│ ├─────────────────────────────────────────────────────┤ │
│ │ Taille du champ      : 50                           │ │
│ │ Format               :                              │ │
│ │ Masque de saisie     :                              │ │
│ │ Légende              :                              │ │
│ │ Valeur par défaut    :                              │ │
│ │ Règle de validation  :                              │ │
│ │ Message si erreur    :                              │ │
│ │ Null interdit        : Non                          │ │
│ │ Chaîne vide autorisée: Oui                          │ │
│ │ Indexé               : Non                          │ │
│ └─────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
```

##### C. Types de données détaillés

| Type | Utilisation | Propriétés |
|------|-------------|------------|
| **Texte court** | Noms, codes, adresses | Taille max 255 car. |
| **Texte long** | Descriptions, commentaires | Illimité |
| **Numérique** | Quantités, mesures | Octet, Entier, Entier long, Réel |
| **NuméroAuto** | Clé primaire auto | Incrémentation ou aléatoire |
| **Date/Heure** | Dates, heures | Formats multiples |
| **Monétaire** | Montants | 4 décimales |
| **Oui/Non** | Choix binaires | Case à cocher |

##### D. Propriétés des champs

###### Propriétés principales

| Propriété | Description | Exemple |
|-----------|-------------|---------|
| **Taille du champ** | Limite de caractères | 50 |
| **Format** | Affichage | Date longue |
| **Masque de saisie** | Format de saisie | (00) 00 00 00 00 |
| **Légende** | Étiquette affichée | Numéro de téléphone |
| **Valeur par défaut** | Valeur initiale | =Date() |
| **Règle de validation** | Condition | >=0 |
| **Message si erreur** | Message d'erreur | "La valeur doit être positive" |
| **Null interdit** | Valeur obligatoire | Oui |
| **Indexé** | Création d'index | Oui (sans doublons) |

##### E. Définition de la clé primaire

**Étapes :**
1. Sélectionner le champ (clic sur la ligne)
2. Clic droit → **Clé primaire**
3. OU Onglet Création → **Clé primaire**

**Symbole :** 🔑 apparaît à gauche du champ

**Bonnes pratiques :**
- Utiliser NuméroAuto pour les clés techniques
- Préférer les valeurs stables
- Éviter les informations signifiantes comme clé

---

#### 💻 TRAVAUX PRATIQUES - Création de tables

**Créer les tables suivantes dans GestionEcole.accdb :**

**Table ETUDIANT :**
| Champ | Type | Taille | Propriétés |
|-------|------|--------|------------|
| NumEtudiant | NuméroAuto | - | Clé primaire |
| Nom | Texte court | 50 | Obligatoire |
| Prenom | Texte court | 50 | Obligatoire |
| DateNaissance | Date/Heure | - | Format Date courte |
| Email | Texte court | 100 | - |
| Telephone | Texte court | 15 | Masque : 00 00 00 00 00 |

**Table CLASSE :**
| Champ | Type | Taille | Propriétés |
|-------|------|--------|------------|
| CodeClasse | Texte court | 10 | Clé primaire |
| Libelle | Texte court | 50 | Obligatoire |
| Niveau | Texte court | 20 | - |
| Effectif | Numérique | Entier | >= 0 |

---

### ☕ PAUSE (14h45 - 15h00)

---

### 🕒 SÉQUENCE 5 : MS Access - Tables Partie 2 (15h00 - 16h30)

**Durée :** 1h30

**Objectif :** Saisir et manipuler des données, import/export

#### Activités

| Temps | Activité | Méthode | Support |
|-------|----------|---------|---------|
| 25 min | Saisie et modification de données | Démonstration + TP | Access |
| 25 min | Validation et masques | Démonstration + TP | Access |
| 25 min | Import/Export | Démonstration + TP | Access + Excel |
| 15 min | Synthèse du jour | Exposé | - |

#### Contenu détaillé

##### A. Mode Feuille de données

**Accès :** Double-clic sur la table OU clic droit → Ouvrir

**Interface :**
```
┌─────────────────────────────────────────────────────────┐
│ NumEtudiant │ Nom        │ Prenom   │ DateNaissance     │
├─────────────┼────────────┼──────────┼───────────────────┤
│ 1           │ DUPONT     │ Marie    │ 15/03/2000        │
│ 2           │ MARTIN     │ Pierre   │ 22/07/1999        │
│ 3           │ DURAND     │ Sophie   │ 08/11/2001        │
│ *           │            │          │                   │ ← Nouvel enreg.
└─────────────────────────────────────────────────────────┘
```

##### B. Saisie de données

###### Ajout d'enregistrements
- Aller à la ligne avec *
- Saisir les valeurs
- Tab pour passer au champ suivant
- Entrée pour valider

###### Modification
- Cliquer sur la cellule
- Modifier la valeur
- Cliquer ailleurs pour valider

###### Suppression
- Sélectionner la ligne (clic sur le sélecteur gauche)
- Touche Suppr ou clic droit → Supprimer

###### Navigation
| Touche | Action |
|--------|--------|
| Tab | Champ suivant |
| Shift+Tab | Champ précédent |
| Ctrl+Home | Premier enregistrement |
| Ctrl+End | Dernier enregistrement |
| F5 | Aller à un enregistrement |

##### C. Règles de validation

###### Validation au niveau du champ

**Propriété "Règle de validation" :**
| Règle | Signification |
|-------|---------------|
| `>0` | Supérieur à 0 |
| `>=1 And <=20` | Entre 1 et 20 |
| `"H" Or "F"` | H ou F seulement |
| `Like "??-###"` | 2 lettres, tiret, 3 chiffres |
| `>=Date()` | Date future ou aujourd'hui |

**Propriété "Message si erreur" :**
Message affiché si la règle n'est pas respectée.

###### Exemple concret
Pour un champ "Note" :
- Règle : `>=0 And <=20`
- Message : "La note doit être comprise entre 0 et 20"

##### D. Masques de saisie

**Définition :** Modèle de saisie guidant l'utilisateur.

**Caractères de masque :**
| Caractère | Signification |
|-----------|---------------|
| 0 | Chiffre obligatoire |
| 9 | Chiffre facultatif |
| # | Chiffre, espace, +, - |
| L | Lettre obligatoire |
| ? | Lettre facultative |
| A | Lettre ou chiffre obligatoire |
| a | Lettre ou chiffre facultatif |
| \\ | Caractère littéral |

**Exemples :**
| Utilisation | Masque | Résultat |
|-------------|--------|----------|
| Téléphone | `00\ 00\ 00\ 00\ 00` | 01 23 45 67 89 |
| Code postal | `00000` | 75001 |
| Date | `00/00/0000` | 15/03/2024 |
| NIR | `0\ 00\ 00\ 00\ 000\ 000` | 1 85 12 75 123 456 |

##### E. Formats d'affichage

###### Formats de date
| Format | Exemple |
|--------|---------|
| Date courte | 15/03/2024 |
| Date longue | vendredi 15 mars 2024 |
| Date moyenne | 15-mars-24 |

###### Formats numériques
| Format | Exemple |
|--------|---------|
| Standard | 1 234,56 |
| Monétaire | 1 234,56 € |
| Pourcentage | 12,34% |
| Scientifique | 1,23E+03 |

##### F. Import/Export de données

###### Import depuis Excel

**Étapes :**
1. Onglet **Données externes** → **Nouvelle source de données** → **À partir d'un fichier** → **Excel**
2. Sélectionner le fichier Excel
3. Choisir : Importer dans nouvelle table OU Ajouter à une table existante
4. Suivre l'assistant
5. Définir les noms de champs (première ligne = en-têtes)
6. Définir la clé primaire
7. Nommer la table

###### Export vers Excel

**Étapes :**
1. Sélectionner la table dans le volet de navigation
2. Onglet **Données externes** → **Excel**
3. Choisir l'emplacement et le nom du fichier
4. Options : Exporter avec mise en forme, Ouvrir après export
5. Cliquer sur OK

###### Autres formats supportés
- CSV (texte délimité)
- XML
- SharePoint
- PDF/XPS (export seulement)
- Base Access externe

---

#### 💻 TRAVAUX PRATIQUES FINAUX

**Exercice 1 : Compléter les tables**

1. Ouvrir la base GestionEcole.accdb
2. Ajouter 5 étudiants dans la table ETUDIANT
3. Ajouter 3 classes dans la table CLASSE
4. Vérifier que les contraintes fonctionnent

**Exercice 2 : Validation et masques**

1. Ajouter un champ "Telephone" à la table ETUDIANT
2. Créer un masque de saisie pour le téléphone
3. Ajouter une règle de validation pour l'effectif de classe (>= 0 et <= 35)

**Exercice 3 : Import**

1. Créer un fichier Excel avec une liste de matières (Code, Libelle, Coefficient)
2. Importer ce fichier dans Access comme nouvelle table MATIERE

---

## ✅ SYNTHÈSE DU JOUR 4

### Points clés à retenir

| Concept | Description |
|---------|-------------|
| **MPD** | Modèle dépendant du SGBD, définit types et contraintes |
| **Types Access** | Texte, Numérique, Date, Monétaire, Oui/Non, etc. |
| **Mode Création** | Meilleur contrôle sur la structure des tables |
| **Clé primaire** | Identifiant unique de chaque enregistrement |
| **Propriétés** | Taille, Format, Masque, Validation, etc. |
| **Import/Export** | Échange de données avec Excel, CSV, etc. |

### Préparation Jour 5
- Tables créées et alimentées
- Questions sur la création de tables
- Préparer des idées de requêtes

---

## 📊 ÉVALUATION DE LA SÉANCE

### Grille d'observation formateur

| Critère | Non acquis | En cours | Acquis |
|---------|------------|----------|--------|
| Compréhension MPD | ☐ | ☐ | ☐ |
| Navigation Access | ☐ | ☐ | ☐ |
| Création tables | ☐ | ☐ | ☐ |
| Configuration champs | ☐ | ☐ | ☐ |
| Saisie de données | ☐ | ☐ | ☐ |
| Import/Export | ☐ | ☐ | ☐ |

### Auto-évaluation participant

1. Je comprends le MPD : ☐ Oui ☐ Partiellement ☐ Non
2. Je sais créer une table Access : ☐ Oui ☐ Partiellement ☐ Non
3. Je maîtrise les propriétés des champs : ☐ Oui ☐ Partiellement ☐ Non
4. Je sais importer des données : ☐ Oui ☐ Partiellement ☐ Non

---

## 📎 DOCUMENTS ANNEXES JOUR 4

- Annexe 4A : Diaporama "MPD et Introduction Access"
- Annexe 4B : Fiche "Types de données Access"
- Annexe 4C : Fiche "Masques de saisie"
- Annexe 4D : Exercices et corrigés Jour 4
- Annexe 4E : Fichier Excel pour import
