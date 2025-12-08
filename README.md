# Ghosts in the Algorithm

This repository contains the project files for **“Ghosts in the Algorithm: Exploring Bias, Radicalization, and Human Choice in AI Recommender Systems”**.  
The project investigates how AI recommendation systems can influence content consumption, potentially amplifying biases or nudging users toward extreme content.

---

## Repository Structure

The repository is organized to separate the report, hands-on activity, references, and documentation:
``` 
IAS_project/
│
├── README.md
|
├── LICENSE 
│
├── report/                     # Final report / blog article
|   |
│   └── figures/                # Plots, diagrams, images for the report
│
├── hands-on-activity/          # Interactive demo code and related materials
|   |
|   ├── streamlit_demo.py       # Main Streamlit simulation script
|   |
│   ├── notebooks/              # Jupyter notebooks for exploration
|   |
│   ├── data/                   # Datasets for simulation (synthetic or Movielens)
|   |
│   └── utils/                  # Helper scripts (SVD, recommendation logic)
│
├── references/                 # Bibliography, papers, articles, reports
|   |
│   └── arxiv_papers/           # Specific research papers from arXiv
│
└── docs/                       # Documentation, tutorials, setup instructions
```

---

## Setup Instructions

1. **Clone the repository**
```bash
git clone git@github.com:up202109000/IAS_project.git
cd IAS_project
```

2. Install Python dependencies (for hands-on activity)
```bash
pip install -r hands-on-activity/requirements.txt
```
   


## Project Deliverables

  Final Report / Blog Article – Documents the case study, analysis, and design of the practical activity.

  Hands-On Activity – Interactive simulation demonstrating user-algorithm interactions and content drift.

## References

Please refer to the references/ folder for research papers, articles, and documents cited in the project.
