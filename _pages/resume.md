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
* **Research Intern**, Kennesaw State University Department of Mathematics (2019)
  * Compared the efficiency of roundabouts, 4-way stops, and traffic lights in semester-long study by observing a 240-vehicle local sample at each intersection type to estimate waiting time distributions
  * Found that a M/M/1 queue accurately modeled traffic light wait times, while a beta distribution more effectively modeled 4-way stops and roundabouts through goodness-of-fit tests in R and Stata
  * Discovered roundabouts had the shortest wait time by 14 seconds through ANOVA and post-hoc tests

* **Teaching Assistant**, Georgia Tech Department of Mathematics (May 2023 − Present)
  * Graded over 500 assignments and exams in three advanced statistics and one partial differential equations class

* **Math and Physics Tutor** − Kennesaw, GA (2019 - 2022)
  * Tutored high school students in math and physics, including SAT Math, achieving a 100% A rate
  
Projects
======
* **Algorithmic Trading in Decentralized Prediction Markets** – Python, SQL, Apache Airflow, Docker, GraphQL
  * Developed a Python algorithm to replicate trades of Ethereum addresses on Polymarket, a decentralized prediction platform, by placing orders on the Central Limit Order Book (CLOB) using a REST API
  * Created an SQL database to track trades by the top 100 forecasters, using GraphQL for querying and Apache Airflow and Docker for an automated data pipeline, accounting for $96 million in trades
  * Discovered that applying the algorithm to expert forecasters produced a 4.5% return after fees in 2022

* **NBA Referee Neutrality Investigation** – Python, pandas, SQL, R, SciPy, Tableau
  * Created 4 metrics for assessing NBA referee bias with a database of 64,000 games preprocessed with SQL, implementing dimensionality reduction and points-over-expected approaches in pandas and R
  * Identified 10 biased referees with points-over-expected metric, finding each had a double-digit point impact (10.00-15.75) on games with selected teams, visualizing findings through Tableau and Datawrapper
  * Discovered zero systemic referee bias in 2004-2022 seasons using propensity score matching with SciPy by controlling for match schedule, winning percentage, and home-court advantage

* **Duplicate Account Detection with NLP** – Python, NLTK, pandas, scikit-learn, SciPy, Matplotlib
  * Developed 3 approaches for identifying duplicate accounts on discussion boards by comparing word frequency, sentence structure, and comment regularity between 600 users with NLTK in Python
  * Preprocessed database of 400,000 forum comments spanning 13 months with pandas and Disqus Web API
  * Achieved a true positive rate of 93% in identifying duplicate accounts with hierarchical cluster analysis in SciPy

* **Quantifying Media Slant: A Computational Method** – Python, PyTorch, Hugging Face, Azure, pandas
  * Created method for quantifying media bias through LLM outputs on Political Compass questions
  * Fine-tuned LLaMA-7B model on dataset of 3,000 articles from 3 news sites with PyTorch on Azure
  * Identified Fox News as the most economically partisan (+3.2), CNN as the highest in social polarization (+2.5), and NPR as exhibiting the least overall bias (aggregate score: 2.9)

  

  
Skills
======
* Languages: Python, SQL, R, C++, Java, MATLAB, Mathematica
* Libraries: pandas, scikit-learn, NLTK, NumPy, SciPy, TensorFlow, PyTorch, Matplotlib
* Tools: Tableau, Azure, Git, Excel, Power BI, MongoDB, Linux, Docker, Snowflake, Apache Airflow, Hadoop


