# 🚀 Jolaan Retail Text-to-SQL RAG System

Un système de RAG (Retrieval-Augmented Generation) et Text-to-SQL de qualité industrielle, conçu pour la plateforme de retail **"Jolaan"**. Il permet aux utilisateurs métiers d'interroger leur base de données en langage naturel (français) tout en garantissant une sécurité stricte (*Secure by Design*).

---

## 🏗️ Architecture & Stack Technique

Le projet respecte les principes de la **Clean Architecture** et des bonnes pratiques **MLOps** :
* **Langage :** Python 3.11 / 3.12
* **API Framework :** FastAPI & Uvicorn
* **Base de données :** ClickHouse (via `clickhouse-connect`)
* **Validation & Configuration :** Pydantic & Pydantic-Settings
* **LLM :** OpenAI API (ou LLM compatible)

---

## 🛡️ Sécurité & Garde-Fous (*Secure by Design*)

Pour éviter toute dérive ou fuite de données en production, le système intègre des barrières strictes :
1. **Principe de Moindre Privilège :** Connexion à ClickHouse configurée exclusivement en **lecture seule (`SELECT`)**.
2. **Liste Blanche des Tables (*Whitelist*) :** Seules les tables autorisées du domaine Ventes peuvent être interrogées.
3. **Protection contre l'Extraction Massive :** Application automatique d'une clause `LIMIT` (maximum 100 lignes par défaut) sur les requêtes générées.

---

## 📊 Périmètre de Données (Phase 1 : Ventes)

Le dictionnaire de données couvre 5 tables principales :
* `entetes` : Tickets de caisse et entêtes de vente.
* `lignes` : Lignes d'articles des tickets.
* `produits` : Catalogue des articles et prix.
* `magasins` : Points de vente et emplacements.
* `fournisseurs` : Gestion des fournisseurs.

---

## ⚙️ Installation et Mise en Route

### 1. Cloner le dépôt et configurer l'environnement virtuel
```bash
# Cloner le projet
git clone <url-du-repo>
cd rag-text-to-sql_clickhouse

# Créer l'environnement virtuel
python -m venv .venv

# Activer l'environnement virtuel
# Sous Windows (PowerShell) :
.\.venv\Scripts\Activate.ps1
# Sous Linux / Mac :
source .venv/bin/activate