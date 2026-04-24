<div align="center">

<img src="https://img.shields.io/badge/Netflix-E50914?style=for-the-badge&logo=netflix&logoColor=white"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
<img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
<img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white"/>

<br><br>

# 🎬 Netflix Data Analysis — EDA Project

> Exploratory Data Analysis on Netflix's content library to uncover trends, genre patterns, and strategic insights from streaming data.

<br>

[![Made With Love](https://img.shields.io/badge/Made%20with-❤️-red?style=flat-square)](/)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()
[![Guided By](https://img.shields.io/badge/Guided%20by-Yash%20Jain-blueviolet?style=flat-square)]()

</div>

---

## 📌 Project Overview

This project performs **Exploratory Data Analysis (EDA)** on the Netflix dataset to uncover insights about content distribution, trends, and viewer preferences.

- 🔍 Analyzes how Netflix's content library has evolved over time
- 📊 Focuses on content type, genre, and release trends
- 💡 Extracts meaningful insights to support content strategy and decision-making

---

## ❓ Problem Statement

With the rapid growth of streaming platforms, understanding content trends is essential. This project analyzes Netflix data to identify patterns in:

| Question | Focus |
|----------|-------|
| 🎥 Content Type | Movies vs TV Shows |
| 📈 Growth Trend | Content added over the years |
| 🌍 Geography | Top content-producing countries |
| 🎭 Genre | Most popular categories |

---

## 📂 Dataset Description

| Column | Description |
|--------|-------------|
| `title` | Name of the content |
| `type` | Movie or TV Show |
| `director` | Director name |
| `cast` | Cast members |
| `country` | Country of production |
| `release_year` | Year of release |
| `rating` | Content rating |
| `duration` | Length of content |
| `listed_in` | Genre / Category |

> ⚠️ Dataset contains missing values in `director`, `cast`, and `country` columns.

---

## 🎯 Objectives

- ✅ Perform data cleaning and preprocessing
- ✅ Conduct detailed Exploratory Data Analysis
- ✅ Identify trends in content distribution
- ✅ Analyze genre and country-wise patterns
- ✅ Generate actionable insights for content strategy

---

## 🛠️ Tools & Technologies

<div align="center">

| Tool | Purpose |
|------|---------|
| 🐍 Python | Core programming language |
| 📓 Jupyter Notebook | Development environment |
| 🐼 Pandas | Data manipulation |
| 🔢 NumPy | Numerical operations |
| 📊 Matplotlib | Data visualization |
| 🎨 Seaborn | Statistical visualization |

</div>

---

## 🧹 Data Preprocessing

```python
# Steps performed
1. Handle missing values  →  director, cast, country
2. Convert data types     →  date_added, release_year
3. Clean categories       →  listed_in, rating
4. Remove duplicates      →  drop_duplicates()
```

---

## 📊 Exploratory Data Analysis

### 🔹 Univariate Analysis
- Distribution of content type (Movies vs TV Shows)
- Rating distribution across titles
- Release year trends

### 🔹 Bivariate Analysis
- Content type vs release trends over time
- Country vs number of titles produced
- Genre vs content popularity

### 🔹 Multivariate Analysis
- Combined analysis of country + genre + release year

---

## 💡 Key Insights

```
🎬  Movies dominate the platform (~70% of all content)
📈  Rapid content growth observed after 2015
🌍  USA & India contribute the majority of content
🎭  Drama and Comedy are the most common genres
```

---

## 📈 Content Growth Timeline

```
Pre-2015  ──●──  Moderate library, mostly licensed content
              │
2015–2017 ──●──  Originals push begins, international expansion
              │
2018–2020 ──●──  Rapid acceleration, regional content rises
              │
  2021+   ──●──  Focus on quality & genre diversity
```

---

## 💼 Business Impact

| Impact Area | Description |
|-------------|-------------|
| 👁️ Viewer Insights | Understand preferences and demand patterns |
| 🛒 Content Acquisition | Data-backed strategy for new content |
| 🌐 Regional Planning | Better planning for underrepresented markets |

---

## 📁 Project Structure

```
📁 Netflix-EDA/
│
├── 📓 03 Netflix.ipynb       ← Main notebook
│     ├── Data Cleaning
│     ├── EDA
│     ├── Visualizations
│     └── Insights
│
└── 📄 README.md
```

---

## 🚀 Future Work

- [ ] 🤖 Build a content recommendation system
- [ ] 🧠 Apply machine learning models for trend prediction
- [ ] 📊 Develop interactive dashboards (Plotly / Power BI)

---

## ▶️ How to Run

```bash
# 1. Clone the repository
git clone https://github.com/your-username/netflix-eda.git

# 2. Navigate to the folder
cd netflix-eda

# 3. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 4. Launch Jupyter Notebook
jupyter notebook
```

---

<div align="center">

### 🙏 Guidance

**Yash Jain** — Future Vision Computer

<br>

⭐ *If you found this project helpful, consider giving it a star!* ⭐

</div>
