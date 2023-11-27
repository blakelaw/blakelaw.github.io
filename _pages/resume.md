---
layout: archive
title: "Résumé"
permalink: /resume/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

<hr class="light-grey-line">

Education
======
* B.S. in Mathematics, Georgia Tech, Expected Spring 2025
* GPA: 3.88
* Concentration: Data Science

Experience
======
* **Incoming Data Science Intern**, Perpay, Philadelphia, PA (2024)

* **Research Intern**, Kennesaw State University Department of Mathematics (2019)
  * Compared the efficiency of roundabouts, 4-way stops, and traffic lights in semester-long study by observing a 240-vehicle local sample at each intersection type to estimate waiting time distributions
  * Found that a M/M/1 queue accurately modeled traffic light wait times, while a beta distribution more effectively modeled 4-way stops and roundabouts through goodness-of-fit tests in R and Stata
  * Discovered roundabouts had the shortest wait time by 14 seconds through ANOVA and post-hoc tests

* **Teaching Assistant**, Georgia Tech Department of Mathematics (May 2023 − Present)
  * Provided feedback for exams and assignments in three advanced statistics and one partial differential class
 
Projects
======

* **NBA Referee Neutrality Investigation** – Python, pandas, Azure, SQL, R, SciPy, Tableau
  * Created 4 metrics to evaluate NBA referee bias using a dataset of 64,000 games processed in Azure SQL Database, employing dimensionality reduction and points-over-expected methods with pandas and R
  * Identified 10 biased referees with points-over-expected metric, finding each had a double-digit point impact (10.00-15.75) on games with selected teams, visualizing findings through Tableau and Datawrapper
  * Discovered zero systemic referee bias in 2004-2022 seasons using propensity score matching with SciPy by controlling for match schedule, winning percentage, and home-court advantage

* **Identifying Cultural Microregions in Georgia** – Python (pandas, scikit-learn), OpenStreetMap
  * Identified over 350 “microregions” in Georgia, small unofficial regions with a common name, by analyzing data from OpenStreetMap (OSM), an open-source geographic data platform
  * Preprocessed over 12 million data points from OSM representing local features using its REST API and pandas
  * Created custom TF-IDF algorithm for similarity scores and used DBSCAN clustering for region identification


* **Duplicate Account Detection with NLP** – Python, NLTK, pandas, scikit-learn, SciPy, Matplotlib 
  * Developed 3 approaches for identifying duplicate accounts on discussion boards by comparing word frequency,
  sentence structure, and comment regularity between 600 users with NLTK in Python
  * Preprocessed 400,000 forum comments over 13 months using PySpark, pandas, and Disqus Web API
  * Achieved a true positive rate of 93% in identifying duplicate accounts with hierarchical cluster analysis in SciPy

* **Quantifying Media Slant: A Computational Method** – Python, PyTorch, pandas, AWS, Databricks
  * Assessed media bias through LLM outputs on Political Compass questions by fine-tuning LLaMA-7B model on dataset of 3,000 articles from 3 news sites using PyTorch on Databricks, backed by AWS EC2 instances
  * Identified Fox News as the most economically partisan (+3.2), CNN as the highest in social polarization (+2.5), and NPR as exhibiting the least overall bias (aggregate score: 2.9)

  

  
Skills
======
* Languages: Python, SQL, R, C++, MATLAB, Mathematica
* Libraries: pandas, scikit-learn, NLTK, NumPy, SciPy, TensorFlow, PyTorch, Matplotlib
* Tools: Tableau, Azure, Excel, Git, MongoDB, AWS, PySpark, Linux, Docker, Snowflake, Databricks, Hadoop, dbt


