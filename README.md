# Enhancing Diversity and Novelty in Book Recommendations

## Project Overview
MSc Data Analytics dissertation analysing 48,871 users and 9,986 books from the Goodbooks-10k (Goodreads) dataset. Built a multi-stage re-ranking pipeline in Python that sits on top of a standard collaborative filtering recommender, aimed at reducing popularity bias and increasing the diversity of book recommendations.

## Dataset
Uses Goodbooks-10k (https://github.com/zygmuntz/goodbooks-10k): 48,871 users, 9,986 books, and rich tag metadata sourced from Goodreads. The four source files (`books.csv`, `to_read.csv`, `tags.csv`, `book_tags.csv`) are included in this repo, in the same folder as the notebook.

## Research Questions Answered
- Does a standard collaborative filtering model over-recommend bestsellers at the expense of lesser-known titles?
- Can post-processing re-ranking improve diversity and novelty without materially hurting accuracy?
- Which re-ranking technique (redundancy removal, popularity adjustment, or topic diversification) contributes most to a better recommendation list?

## Key Findings
- **Diversity improved significantly**: Intra-List Similarity dropped from 0.132 to 0.091 (p < 0.01)
- **Accuracy trade-off was minor**: Precision@10 fell only from 0.0056 to 0.0052
- **Popularity bias was reduced**: recommendations shifted measurably away from "Head" bestsellers toward long-tail titles
- **λ = 0.85 is the sweet spot**: balances diversity gains against accuracy loss for both MMR and X-QuAD stages
- **Multi-stage re-ranking works well in sequence**: MMR, popularity adjustment, and X-QuAD each address a distinct weakness of standard collaborative filtering

## Tools & Technologies
| Tool | Usage |
|---|---|
| Python (Pandas, NumPy, SciPy) | Data cleaning, EDA, sparse matrix operations |
| Scikit-learn | Preprocessing, similarity computation |
| Matplotlib & Seaborn | Data visualisation |
| Goodbooks-10k (Goodreads) | Source dataset |

## Methodology
1. **IBCF (baseline)**: item-item collaborative filtering using cosine similarity on user "to-read" interactions
2. **MMR**: removes near-duplicate recommendations
3. **Popularity Adjustment**: down-weights bestsellers to surface lesser-known titles
4. **X-QuAD**: uses Goodreads tags to diversify recommendations across genres/themes

## Results
| Model | Precision@10 | Recall@10 | ILS@10 (Diversity, lower is better) | Coverage (Novelty) |
|---|---|---|---|---|
| IBCF Only (baseline) | 0.0056 | 0.0275 | 0.132 | 0.953 |
| Full Pipeline (tuned) | 0.0052 | 0.0256 | **0.091** | 0.920 |

Full figures (EDA, hyperparameter tuning, and case study walkthrough) are in the dissertation PDF (`dissertation.pdf`).

## Project Structure
```
book-recommendation-reranking/
│
├── dissertation.pdf
├── notebook.ipynb
├── books.csv
├── to_read.csv
├── tags.csv
├── book_tags.csv
|── Images/
│   ├── pipeline_architecture.png
│   └── results_diversity_novelty.png
└── README.md
```

## How To Run
1. Clone the repository
2. Install dependencies: `pip install pandas numpy scipy scikit-learn matplotlib seaborn`
3. Open `notebook.ipynb` in Jupyter (the CSV files are already included in the repo, in the same folder as the notebook)
4. Run cells sequentially

## Author
Pranali Deore
MSc Data Analytics, Queen Mary University of London
LinkedIn: https://linkedin.com/in/deorepranali
