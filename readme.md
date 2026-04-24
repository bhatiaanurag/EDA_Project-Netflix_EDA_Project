<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=E50914&height=220&section=header&text=Netflix%20Data%20Analysis&fontSize=50&fontColor=ffffff&fontAlignY=38&desc=Exploratory%20Data%20Analysis%20Project&descAlignY=58&descSize=20&descColor=ffcccc&animation=fadeIn" width="100%"/>

<br>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&duration=3000&pause=1000&color=E50914&center=true&vCenter=true&width=600&lines=Netflix+Content+Analysis;Exploratory+Data+Analysis+(EDA);Uncovering+Streaming+Trends;Data-Driven+Content+Strategy" alt="Typing SVG" />

<br><br>

<img src="https://img.shields.io/badge/Netflix-E50914?style=for-the-badge&logo=netflix&logoColor=white"/>
&nbsp;
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
&nbsp;
<img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
&nbsp;
<img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
&nbsp;
<img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white"/>
&nbsp;
<img src="https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge&logo=python&logoColor=white"/>

<br><br>

<img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square"/>
&nbsp;
<img src="https://img.shields.io/badge/Language-Python%203.x-blue?style=flat-square"/>
&nbsp;
<img src="https://img.shields.io/badge/Domain-Data%20Science-orange?style=flat-square"/>
&nbsp;
<img src="https://img.shields.io/badge/Type-EDA-purple?style=flat-square"/>

<br><br>

<img src="https://komarev.com/ghpvc/?username=netflix-eda&label=Profile+Views&color=E50914&style=flat-square" alt="views"/>

<br><br>

</div>

---

## Overview

This project performs **Exploratory Data Analysis (EDA)** on the Netflix dataset to uncover insights about content distribution, trends, and viewer preferences. The analysis focuses on understanding how Netflix's content library has evolved over time and extracting meaningful insights that can support content strategy and decision-making.

---

## Problem Statement

With the rapid growth of streaming platforms, understanding content trends has become essential for competitive strategy. This project systematically analyzes Netflix data to identify patterns across content type, genre, geography, and release timelines.

<br>

<div align="center">

| Question | Area of Focus |
|:--------:|:-------------:|
| What type of content is more prevalent? | Movies vs TV Shows |
| How has content grown over the years? | Release Year Trends |
| Which countries produce the most content? | Geographic Distribution |
| What are the most popular genres? | Genre Analysis |

</div>

---

## Dataset Description

<div align="center">

| Column | Type | Description |
|--------|------|-------------|
| `title` | String | Name of the content |
| `type` | Categorical | Movie or TV Show |
| `director` | String | Director name (has missing values) |
| `cast` | String | Cast members (has missing values) |
| `country` | Categorical | Country of production (has missing values) |
| `release_year` | Integer | Year of original release |
| `rating` | Categorical | Content maturity rating |
| `duration` | String | Runtime in minutes or seasons |
| `listed_in` | String | Genre / Category tags |

</div>

> The dataset is a combination of categorical and numerical variables and contains missing values that require preprocessing before analysis.

---

## Objectives

<img align="right" alt="Analysis" width="320" src="https://raw.githubusercontent.com/abhisheknaiidu/abhisheknaiidu/master/code.gif"/>

- Perform thorough data cleaning and preprocessing
- Conduct detailed Exploratory Data Analysis at univariate, bivariate, and multivariate levels
- Identify trends in content distribution across time
- Analyze genre and country-wise content patterns
- Generate actionable insights for content strategy

<br><br><br><br>

---

## Tools & Technologies

<div align="center">

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.x | Core programming language |
| Jupyter Notebook | Latest | Development & documentation environment |
| Pandas | Latest | Data manipulation and analysis |
| NumPy | Latest | Numerical operations |
| Matplotlib | Latest | Base plotting and visualization |
| Seaborn | Latest | Statistical data visualization |

<br>

<img src="https://skillicons.dev/icons?i=python&theme=dark" height="40"/>
&nbsp;&nbsp;
<img src="https://skillicons.dev/icons?i=github&theme=dark" height="40"/>
&nbsp;&nbsp;
<img src="https://skillicons.dev/icons?i=vscode&theme=dark" height="40"/>

</div>

---

## Exploratory Data Analysis

### Univariate Analysis
- Distribution of content type — Movies vs TV Shows
- Rating distribution across all titles
- Frequency of content by release year

### Bivariate Analysis
- Content type trends over release years
- Country-wise count of titles produced
- Genre popularity across the platform

### Multivariate Analysis
- Combined analysis of country, genre, and release year
- Cross-tabulation of content type and rating
- Heatmaps for correlation and category intersections

---

## Key Insights

```
01  Movies dominate the platform, accounting for approximately 70% of all content.

02  Rapid content growth was observed post-2015, coinciding with Netflix's
    aggressive push into original productions and international markets.

03  A small number of countries — primarily the United States and India —
    contribute the majority of titles available on the platform.

04  Drama and Comedy are the most common genres, reflecting consistent
    viewer demand for narrative and entertainment-driven content.
```

---

## Content Growth Timeline

```
  Pre-2015  |  Moderate library with primarily licensed third-party content
            |
  2015-2017  |  Originals strategy launched — international expansion begins
            |
  2018-2020  |  Rapid acceleration — India, South Korea, and Europe rise
            |
    2021+   |  Catalog maturation — focus shifts to quality over quantity
```

---

## Business Impact

<div align="center">

| Area | Impact |
|------|--------|
| Viewer Understanding | Identifies preferences and demand patterns from real data |
| Content Acquisition | Supports data-driven decisions on what content to acquire |
| Regional Strategy | Highlights opportunities in underrepresented markets |
| Genre Planning | Guides investment toward high-performing genre categories |

</div>

---

## Project Structure

```
Netflix-EDA/
│
├── 03 Netflix.ipynb          # Main analysis notebook
│     ├── Section 1           # Data loading & cleaning
│     ├── Section 2           # Exploratory Data Analysis
│     ├── Section 3           # Visualizations
│     └── Section 4           # Insights & Conclusions
│
└── README.md                 # Project documentation
```

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/your-username/netflix-eda.git

# Navigate into the project directory
cd netflix-eda

# Install required dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Launch Jupyter Notebook
jupyter notebook
```

---

## Future Work

- [ ] Build a content-based recommendation system using NLP on descriptions
- [ ] Apply machine learning models to predict genre popularity trends
- [ ] Develop an interactive dashboard using Plotly or Power BI
- [ ] Perform sentiment analysis on user reviews for qualitative insights

---

## Conclusion

The analysis provides a structured view of Netflix's content evolution and highlights clear trends in content type, geography, and genre preference. These insights can directly support content acquisition decisions, regional planning efforts, and viewer engagement strategies.

---

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=16&duration=4000&pause=1000&color=E50914&center=true&vCenter=true&width=500&lines=Thank+you+for+visiting!;Star+the+repo+if+you+found+it+helpful!" alt="Typing SVG" />

<br>

**Guided by Yash Jain — Future Vision Computer**

<br>

![](https://img.shields.io/badge/If%20you%20found%20this%20helpful-Star%20the%20repo-E50914?style=for-the-badge)

</div>
