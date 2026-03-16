# Data and Analysis
 
This repository contains the anonymized data and analysis code for the paper *["Investigating the Effects of LLM Use on Critical Thinking Under Time Constraints: Access Timing and Time Availability"](https://doi.org/10.1145/3772318.3791796)*.
 
---
 
## Repository Structure
 
```
├── README.md
├── study_data/
│   ├── main_study_data.xlsx              # Primary per-participant study data (n = 393)
│   ├── essay_graded.xlsx                 # Essay performance scores (n = 393)
│   └── recall_graded.xlsx                # Recall performance scores (n = 393)
├── behavioral_log_based_data/
│   ├── argument_and_referenced_docs_overlap.xlsx   # Argument and document reference overlap (n = 393)
│   ├── copy_rate_and_textual_overlap.xlsx          # Text copying and AI-essay textual overlap (n = 393)
│   ├── early_access_data.xlsx                      # Behavioral logs for Early AI access conditions (n = 90)
│   ├── late_access_data.xlsx                       # Behavioral logs for Late AI access conditions (n = 98)
│   └── task_approaches.xlsx                        # Qualitative coding of AI task approach strategies (n = 393)
├── main_results_plots/                   # Generated plots from main analyses
├── behavioral_engagement_plots/          # Generated plots from behavioral analyses
├── Critical_Thinking_Main_Analyses.Rmd   # Main statistical analyses
└── Critical_Thinking_Behavioral_Analyses.Rmd  # Descriptive analyses of log-based behavioral metrics
```
 
---
 
## Data
 
### Study Design
 
Participants (N = 393) were recruited via Prolific and completed a [critical thinking task](https://doi.org/10.3389/feduc.2020.00156). The study used a **4 x 2 between-subjects design**:
 
- **LLM Access Timing** (4 levels): Early, Continuous, Late, No LLM access
- **Time Availability** (2 levels): Insufficient (10 min), Sufficient (30 min)
 
### Study Data
 
| File | Description |
|---|---|
| `main_study_data.xlsx` | Primary per-participant dataset containing experimental conditions, study responses, interaction logs, self-report measures, and demographics |
| `essay_graded.xlsx` | Essay scores |
| `recall_graded.xlsx` | Recall scores |
 
The interaction logs in `main_study_data.xlsx` capture event types and counts, temporal information, and time allocation metrics across interface panels. These logs enable deriving log-based behavioral metrics at different granularities, supporting analysis of how participants moved between reading, using the LLM, and writing throughout the task, and further processing. Such derivations are performed in `Critical_Thinking_Behavioral_Analyses.Rmd`.
 
A full description of all columns in `main_study_data.xlsx` is available in the [data dictionary](https://github.com/xxxxbrandieeee/critical-thinking-data-dictionary).
 
### Behavioral Log-Based Data
 
These behavioral metrics are further processed from the interaction logs through comparison, computation, and qualitative coding, each focusing on a specific aspect of participant behavior.
 
| File | n | Description |
|---|---|---|
| `argument_and_referenced_docs_overlap.xlsx` | 393 | Overlap between arguments in participants' essays and LLM responses, and between documents referenced in essays and LLM responses |
| `copy_rate_and_textual_overlap.xlsx` | 393 | Rates of text copied from LLM responses, and textual overlap between participants' essays and LLM responses |
| `early_access_data.xlsx` | 90 | Interaction logs for participants in Early LLM access conditions, enabling analysis of changes in behavioral metrics relative to when the LLM was introduced |
| `late_access_data.xlsx` | 98 | Interaction logs for participants in Late LLM access conditions, enabling analysis of changes in behavioral metrics relative to when the LLM was introduced |
| `task_approaches.xlsx` | 393 | Participants' task approaches, coded based on open-ended responses |
 
---
 
## Analysis
 
### Requirements
 
R (≥ 4.1) with the following packages:
 
```r
install.packages(c("tidyverse", "readxl", "janitor", "car", "emmeans",
                   "gtsummary", "ggtext", "scales", "patchwork", "ggpattern"))
```
 
### Analysis Scripts
 
**`Critical_Thinking_Main_Analyses.Rmd`**
 
Primary statistical analyses reported in the paper. Uses data from `study_data/`.
 
- Loads and merges the primary dataset with essay and recall graded scores; derives experimental factors (`time_availability`, `ai_access`) and recodes covariates (LLM familiarity, attitude, self-efficacy, AI confidence) to numeric scales
- Runs two-way ANCOVAs (Time Availability × LLM Access) with Type III sums of squares for each dependent variable: essay total score, number of arguments, myside bias, recall, evaluation (relevance, trustworthiness, stance, total), and comprehension; conducts Tukey HSD post-hoc comparisons when significant main or interaction effects are found
- Generates plots for all dependent variables (saved to `main_results_plots/`)
- Reports descriptive statistics and Mann-Whitney U tests (with Bonferroni correction) for self-assessment of critical thinking ratings
 
**`Critical_Thinking_Behavioral_Analyses.Rmd`**
 
Descriptive analyses of log-based behavioral metrics. Uses data from both `study_data/` and `behavioral_log_based_data/`.
 
- Derives log-based behavioral metrics at varying granularities from the interaction logs in `main_study_data.xlsx`
- Summarizes argument and document reference overlap between participants' essays and LLM responses
- Summarizes Early and Late LLM access conditions for changes in behavioral metrics relative to LLM injection timing
- Summarizes text copying rates and textual overlap between participants' essays and LLM responses
- Generates plots for behavioral engagement (saved to `behavioral_engagement_plots/`)
- Summarizes qualitative coding of task approach strategies by condition
 
