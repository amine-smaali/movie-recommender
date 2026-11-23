# Movie Recommendation System

A content-based movie recommender built with Python. Give it a movie title and it returns the 5 most similar movies from the TMDB 5000 dataset.

## How it works

Each movie is described by one block of text ("tags") made of:

- plot overview words
- genres
- keywords
- top 3 cast members
- director

The pipeline:

1. **Load and merge** the movies and credits datasets
2. **Clean** missing values and duplicates
3. **Parse** the JSON-like columns (genres, keywords, cast, crew) into lists of names
4. **Build tags** by combining all features into one text per movie
5. **Stem** the words with `PorterStemmer` (so "loving" and "loved" match)
6. **Vectorize** with `CountVectorizer` (5000 most common words, English stop words removed)
7. **Compare** every pair of movies with cosine similarity
8. **Recommend** the movies with the highest similarity score

## Dataset

[TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata) from Kaggle. Download these two files and place them in the project folder next to the notebook:

- `tmdb_5000_movies.csv`
- `tmdb_5000_credits.csv`

## Installation

```bash
pip install pandas scikit-learn nltk jupyter
```

## Usage

1. Open the notebook:
   ```bash
   jupyter notebook MovieRecommendation_commented.ipynb
   ```
2. Run all cells.
3. Call the function with any movie title from the dataset:
   ```python
   recommend("Falcon Rising")
   ```

The function prints the 5 most similar titles.

## Project structure

```
.
├── MovieRecommendation_commented.ipynb
├── tmdb_5000_movies.csv
├── tmdb_5000_credits.csv
└── README.md
```

## Possible improvements

- Use `TfidfVectorizer` instead of raw word counts
- Give more weight to genres, keywords and director
- Merge the datasets on movie id instead of title
- Handle titles that are not found in the dataset
- Save the similarity matrix with `pickle` to avoid recomputing it
- Build a web interface with Streamlit or Flask

## Tech stack

Python, pandas, scikit-learn, NLTK
