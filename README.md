# 📚 Semantic Book Recommender

Un système de recommandation de livres intelligent qui utilise la **recherche sémantique** et les **Large Language Models (LLMs)** pour aider les lecteurs à découvrir leur prochain coup de cœur littéraire.

Ce projet est basé sur le tutoriel de [Jodie Burchell (JetBrains)](https://github.com/t-redactyl/llm-semantic-book-recommender) et adapté pour fonctionner avec des modèles **open-source gratuits** (Hugging Face) au lieu d'OpenAI.

---

## 🎯 Objectif du projet

Construire un moteur de recommandation qui ne se base **pas** sur les notes des utilisateurs, mais sur le **sens même des descriptions de livres**. L'utilisateur peut :

- 🔍 Décrire le type de livre qu'il cherche ("une histoire sur le pardon")
- 🏷️ Filtrer par catégorie (Fiction, Nonfiction, Children's Fiction, Children's Nonfiction)
- 😊 Filtrer par ton émotionnel (Joyeux, Surprenant, Triste, Effrayant, Colérique)

Le système retourne ensuite une sélection personnalisée de 16 livres avec leurs couvertures.

---

## 🧠 Concepts clés utilisés

| Concept | Description |
|---|---|
| **Embeddings** | Transformation des descriptions de livres en vecteurs mathématiques qui capturent leur sens |
| **Recherche vectorielle** | Trouver les livres dont les vecteurs sont les plus proches d'une requête |
| **Zero-shot classification** | Classer des livres dans des catégories sans entraînement spécifique |
| **Analyse d'émotions** | Détecter les émotions dominantes (joie, peur, tristesse...) dans les descriptions |
| **Dashboard Gradio** | Interface web interactive pour l'utilisateur final |

---

## 🛠️ Outils et technologies utilisés

### Langages et environnements
- **Python 3.11+** — Langage principal
- **Jupyter Notebook** — Pour l'exploration et le prototypage
- **VS Code** — Éditeur de code
- **Git & GitHub** — Versionnement

### Bibliothèques principales

| Bibliothèque | Rôle |
|---|---|
| **pandas** | Manipulation des données tabulaires |
| **numpy** | Calcul numérique |
| **seaborn / matplotlib** | Visualisation des données |
| **transformers** (Hugging Face) | Modèles de NLP (classification, émotions) |
| **sentence-transformers** | Génération d'embeddings gratuits |
| **langchain** | Framework pour orchestrer les LLMs |
| **chromadb** | Base de données vectorielle pour la recherche sémantique |
| **gradio** | Création du dashboard web |
| **python-dotenv** | Gestion des variables d'environnement |

### Modèles utilisés (tous open-source et gratuits)

| Modèle | Tâche |
|---|---|
| `sentence-transformers/all-MiniLM-L6-v2` | Génération d'embeddings |
| `cross-encoder/nli-MiniLM2-L6-H768` | Classification Fiction/Nonfiction |
| `j-hartmann/emotion-english-distilroberta-base` | Détection d'émotions |

### Source des données
- **Dataset** : [7K Books with Metadata](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata) par Dylan Castillo (Kaggle)
- **Taille** : ~6 800 livres avec titre, auteur, description, note, etc.

---

## 🚀 Étapes du projet

### 📦 Partie 1 — Préparation des données

**Notebook** : `1_data_preparation.ipynb`

1. Téléchargement du dataset depuis Kaggle
2. Nettoyage des données :
   - Suppression des livres sans description
   - Suppression des descriptions trop courtes (< 25 mots)
   - Gestion des valeurs manquantes
3. Création d'un fichier `tagged_description.txt` (ISBN + description par ligne)
4. Création d'une base vectorielle **Chroma** avec les embeddings

**Résultat** : Un dataset propre et une base vectorielle interrogeable.

### 📦 Partie 2 — Catégorisation des livres

**Notebook** : `2_text_classification.ipynb`

1. Analyse des 479 catégories existantes
2. Création d'un mapping manuel vers 4 catégories simples :
   - Fiction
   - Nonfiction
   - Children's Fiction
   - Children's Nonfiction
3. Classification zero-shot pour les 1454 livres sans catégorie
4. Évaluation de la précision : **77.8%**

**Résultat** : Un fichier `books_with_categories.csv` avec une colonne `simple_categories` complète.

### 📦 Partie 3 — Analyse émotionnelle

**Notebook** : `3_emotion_analysis.ipynb`

1. Chargement du modèle d'émotions (`j-hartmann/emotion-english-distilroberta-base`)
2. Découpage des descriptions en phrases
3. Classification de chaque phrase en 7 émotions :
   - anger, disgust, fear, joy, sadness, surprise, neutral
4. Extraction du score maximum par émotion pour chaque livre

**Résultat** : Un fichier `books_with_emotions.csv` avec 7 colonnes d'émotions.

### 📦 Partie 4 — Dashboard interactif

**Script** : `gradio-dashboard.py`

1. Chargement des données enrichies
2. Création de la base vectorielle
3. Interface utilisateur avec 3 entrées :
   - Description recherchée
   - Catégorie
   - Ton émotionnel
4. Affichage des 16 recommandations sous forme de galerie

**Résultat** : Une application web fonctionnelle.

---

## ⚙️ Installation et lancement

### Prérequis
- Python 3.11 ou supérieur
- Git
- Un environnement virtuel (recommandé)

### Étapes

```bash
# 1. Cloner le dépôt
git clone https://github.com/MariemMhadhbii/Semantic-Book-Recommender.git
cd Semantic-Book-Recommender

# 2. Créer un environnement virtuel
python -m venv .venv

# 3. Activer l'environnement virtuel
# Sur Windows :
.venv\Scripts\activate
# Sur Mac/Linux :
source .venv/bin/activate

# 4. Installer les dépendances
pip install -r requirements.txt

# 5. Lancer le dashboard
python gradio-dashboard.py
```



📬 Contact
Mariem Mhadhbi

GitHub : @MariemMhadhbii

Email : mhadhbiimariem@gmail.com
