# 🏥 OncoPlatCI — Plateforme Big Data pour l'analyse des données de dépistage du cancer en Côte d'Ivoire

> **Mémoire de fin de cycle — Master Data Engineering | ISAE-ISM Paris | 2025-2026**  
> Groupe DI24GP2 · Chef de groupe & contributeur principal : **BEAKOU AHIPAUD Emmanuel**  
> Encadrant : Dr. TOKPAN · Soutenance : Juin 2026

---

## 📌 Contexte & Problématique

La Côte d'Ivoire recense plus de **28 000 nouveaux cas de cancer par an** (OMS/GLOBOCAN 2022), dont **67% diagnostiqués au stade avancé (III–IV)**, faute de centralisation des données oncologiques.

| Indicateur | Valeur |
|---|---|
| Nouveaux cas/an | 28 000+ |
| Décès estimés/an | 22 000+ |
| Patients diagnostiqués trop tard | 67% (stade III–IV) |
| Délai moyen de diagnostic | 47 jours (OMS : 30 j) |
| Écart territorial | 35 j (Abidjan) vs 72 j (Man) |
| Sites de données fragmentés | 53 sites EGPAF + 4 CHU — aucune consolidation |

**Réponse : OncoPlatCI** — une plateforme Big Data complète, déployable **offline sur tablettes Android CHU ivoiriens (482 KB)**, couvrant les 10 régions sanitaires du pays.

---

## 🎯 Objectifs du projet

| Plan | Objectif | Résultat | Note |
|---|---|---|---|
| A1 | Collecte & Feature Engineering | 1 020 000 patients · 98,2% complétude · 14 191 doublons traités | 4,90/5 |
| A2 | Architecture & Pipeline ETL | Data Lake 3 zones · Airflow @daily · 4/4 tâches automatisées | 4,50/5 |
| A3 | Analyse Épidémiologique | Kaplan-Meier · Carte 10 régions · Tendances 2015–2024 | 4,30/5 |
| A4 | Machine Learning | AUC-ROC **0,891** · F1-Score **0,863** · SHAP explicable | 4,00/5 |
| A5 | Plateforme OncoPlatCI | 14 modules · 482 KB · Offline · 33 aides contextuelles | 4,50/5 |

**Note moyenne globale : 4,44 / 5 — tous objectifs atteints ou dépassés.**

---

## 🏗️ Architecture de la solution

```
┌─────────────────────────────────────────────────────────┐
│                    SOURCES DE DONNÉES                   │
│        OMS/GLOBOCAN 2022 · EGPAF · CHU · MSHPCMU        │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│               PIPELINE ETL — Apache Airflow             │
│         Ingestion → Nettoyage → Transformation          │
└────────────┬──────────────┬──────────────┬──────────────┘
             │              │              │
             ▼              ▼              ▼
        🥉 BRONZE      🥈 SILVER      🥇 GOLD
        (Raw Data)   (Cleaned Data) (Aggregated)
             │              │              │
             └──────────────┴──────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│              ANALYSE & MACHINE LEARNING                 │
│   PySpark · Scikit-learn · Random Forest · SHAP         │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│               PLATEFORME OncoPlatCI                     │
│          14 modules · Offline · 482 KB Android          │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Stack technique

| Catégorie | Technologies |
|---|---|
| Langages | Python · SQL |
| Big Data & ETL | Apache Airflow · Apache PySpark |
| Machine Learning | Scikit-learn · Random Forest · SHAP |
| Analyse statistique | Kaplan-Meier (lifelines) · Scipy |
| Visualisation | Matplotlib · Seaborn · SVG interactif |
| Base de données | MySQL |
| Environnement | Jupyter Notebook · Google Colab |
| Versionning | Git · GitHub |

---

## 📊 Résultats Machine Learning

```
Comparaison des modèles testés :

Modèle 1 (Baseline)     AUC-ROC : 0.34  ██░░░░░░░░
Modèle 2 (Amélioré)     AUC-ROC : 0.63  ██████░░░░
Modèle 3 Random Forest  AUC-ROC : 0.891 █████████░  ✅ Retenu

F1-Score final : 0.863  (+15,1% vs objectif)
Objectif initial : AUC-ROC ≥ 0.80  → Dépassé de +11,4%
```

**Top 6 variables SHAP (explicabilité du modèle) :**
1. Stade au diagnostic
2. Délai de prise en charge
3. Région sanitaire
4. Type de cancer
5. Âge du patient
6. Accès au centre de soins

---

## 🗺️ Analyse épidémiologique

- **Survie Kaplan-Meier** : 79% à 5 ans (Stade I) vs 23% (Stade IV)
- **10 régions sanitaires** cartographiées avec alertes OMS
- **Inégalités territoriales** : délai 35j (Abidjan) → 72j (Man), mortalité 22% → 40%
- **Tendances 2015–2024** analysées sur l'ensemble du territoire

---

## 📱 Plateforme OncoPlatCI — 14 modules

### 7 modules standards
| # | Module | Description |
|---|---|---|
| 01 | Tableau de bord | Vue synthétique des indicateurs clés |
| 02 | Gestion patients | Dossiers patients complets |
| 03 | Saisie dépistage | Formulaires de collecte terrain |
| 04 | Statistiques | Analyses et graphiques |
| 05 | Historique | Suivi longitudinal |
| 06 | Paramètres | Configuration système |
| 07 | Utilisateurs | Gestion des accès |

### 7 modules avancés inédits ⭐
| # | Module | Inspiré de | Description |
|---|---|---|---|
| 08 | Carte Géospatiale | WHO DHIS2 | SVG interactive · 10 régions · alertes OMS |
| 09 | Score Risque IA | IBM Watson Oncology | Jauge 0–97% · 6 barres SHAP |
| 10 | Alertes Cliniques | Epic CDS | 8 alertes auto · 3 niveaux · journal d'audit |
| 11 | Parcours de Soins | NHS Care Pathways | 5 étapes CI vs OMS · goulots identifiés |
| 12 | App Terrain | WHO DHIS2 Mobile | Offline · QR · GPS · synchro SIGDEP |
| 13 | Dashboard Exécutif | NHS Digital / Palantir | 6 KPIs · export PDF/JSON |
| 14 | Portail Patient | Epic MyChart | SMS 25 FCFA Orange CI · WhatsApp |

---

## 👥 Équipe — Groupe DI24GP2

| Membre | Matricule | Rôle |
|---|---|---|
| **BEAKOU AHIPAUD Emmanuel** | ISMDI24UB7156 | **Chef de groupe · Contributeur principal** |
| KOUASSI KONAN Simplice | ISMDI24UB769 | Membre |
| ACHI Jean-Philippe | ISMDI24UB084 | Membre |
| HASSAN AHMED Zam-Zam | ISMDI24UB904 | Membre |
| BADIEL Lucien | ISMDI24UB903 | Membre |

---

## 🚀 Roadmap 2026–2030

| Période | Étape |
|---|---|
| 2026–2027 | Partenariat CHU Cocody — intégration données réelles |
| 2027 | Intégration HL7 FHIR R4 (labo, pharmacies, CMU) |
| 2028+ | Extension CEDEAO — Sénégal, Burkina Faso, Mali, Ghana |
| 2030 | Biomarqueurs HER2, BRCA, PDL1 — médecine de précision |

---

## 📚 Références

- GLOBOCAN 2022 — WHO/IARC — [iarc.who.int](https://iarc.who.int)
- OMS — Rapport cancer Afrique subsaharienne, 2023 — [who.int](https://who.int)
- Apache Airflow — [airflow.apache.org](https://airflow.apache.org)
- Apache Spark — [spark.apache.org](https://spark.apache.org)
- Lundberg & Lee — SHAP: A Unified Approach, NeurIPS 2017
- Kaplan & Meier — Nonparametric estimation, JASA, 1958

---

## 📬 Contact

**BEAKOU AHIPAUD Emmanuel**  
📧 Ahipaudbeakou@gmail.com  
📞 +225 0757 206 123  
🔗 [linkedin.com/in/ahipaud-emmanuelbeakou](https://linkedin.com/in/ahipaud-emmanuelbeakou)

---

*ISAE-ISM Paris Executive Education · Master Data Engineering — CAF · 2025-2026*
