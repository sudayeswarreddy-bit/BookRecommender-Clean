# 📚 Book Recommender System

A web-based book recommendation app built with **Python and Flask**. It shows the most popular books on the home page and, given a book title, recommends similar books using **item-based collaborative filtering**.

## Features

- **Top books** – the home page lists popular books with cover image, author, number of ratings and average rating.
- **Book recommendations** – enter a book title and get 4 similar books with title, author and cover.
- **Pre-computed model** – the similarity data is stored in pickle files, so recommendations are returned quickly without retraining at request time.
- **Deployment-ready** – includes a `Procfile` and `gunicorn` for hosting on platforms such as Heroku or Render.

## How It Works

1. **Data preparation** (see `book-recommender-system.ipynb`)
   - Books, users and ratings data are cleaned and merged.
   - **Popularity-based list:** books are ranked using their number of ratings and average rating → `popular.pkl`.
2. **Collaborative filtering**
   - A pivot table of book titles × users (ratings as values) is built → `pt.pkl`.
   - A similarity matrix is computed between all books in the pivot table → `similarity_scores.pkl`.
3. **Serving recommendations** (`app.py`)
   - The selected title is looked up in the pivot table.
   - Its similarity scores are sorted, and the 4 closest books (excluding the book itself) are returned with metadata from `books.pkl`.

## Tech Stack

| Area | Tools |
| --- | --- |
| Language | Python |
| Web framework | Flask |
| Data processing | pandas, NumPy |
| Frontend | HTML templates (Jinja2) |
| Deployment | gunicorn, Procfile |

## Project Structure

```
BookRecommender-Clean/
├── templates/                      # HTML templates (index.html, recommend.html)
├── app.py                          # Flask application and routes
├── book-recommender-system.ipynb   # Data cleaning, analysis and model building
├── books.pkl                       # Book metadata (title, author, image URL)
├── popular.pkl                     # Popular books dataframe
├── pt.pkl                          # Pivot table (books × users)
├── similarity_scores.pkl           # Book-to-book similarity matrix
├── requirements.txt                # Python dependencies
├── Procfile                        # Process file for deployment
└── .gitignore
```

## Routes

| Route | Method | Description |
| --- | --- | --- |
| `/` | GET | Home page showing popular books |
| `/recommend` | GET | Recommendation search page |
| `/recommend_books` | POST | Returns 4 books similar to the entered title |

## Getting Started

### Prerequisites

- Python 3.8+
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/sudayeswarreddy-bit/BookRecommender-Clean.git
cd BookRecommender-Clean

# (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Run locally

```bash
python app.py
```

Then open **http://127.0.0.1:5000** in your browser.

### Run in production

```bash
gunicorn app:app
```

## Usage

1. Open the home page to browse the most popular books.
2. Go to the **Recommend** page.
3. Type the exact title of a book from the dataset and submit.
4. View four similar book recommendations.

> **Note:** Titles must match the dataset exactly. Only books that have enough ratings to appear in the pivot table can be used as input.

## Future Improvements

- Add a search box with title suggestions / autocomplete.
- Handle titles that are not found with a friendly error message instead of a server error.
- Add content-based filtering to cover books with few ratings.
- Add a Dockerfile and live demo link.

## Author

**S. Udayeswar Reddy**
