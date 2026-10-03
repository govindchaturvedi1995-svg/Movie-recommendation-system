# 🎬 Movie Recommender System

A content-based movie recommendation web app built with **Python**, **Streamlit**, **Pandas**, and **Scikit-learn**. Select a movie and discover five movies with similar genres, keywords, and plot descriptions. The app can also display movie posters using the OMDb API.

**GitHub repository:** https://github.com/govindchaturvedi1995-svg/Movie-recommendation-system

---

## ✨ Features

- **Movie selection:** Choose a title from the movie dataset.
- **Content-based recommendations:** Suggests five similar movies based on movie metadata.
- **Text processing:** Combines genres, keywords, and overview text into a single feature set.
- **Similarity calculation:** Uses `CountVectorizer` and cosine similarity.
- **Movie posters:** Retrieves poster images from the OMDb API when available.
- **Streamlit interface:** Interactive web app with a custom dark-gradient theme.
- **Deployable:** Can run locally or be deployed with Streamlit Community Cloud.

## 🧰 Tech stack

- Python
- Streamlit
- Pandas
- Scikit-learn
- Requests
- TMDB 5000 Movies dataset
- OMDb API (for poster images)

## 📁 Project structure

```text
movie-recommender-system/
├── streamlit_app.py
├── tmdb_5000_movies.csv
├── requirements.txt
├── README.md
└── .gitignore
```

Keep the CSV dataset in the same directory as `streamlit_app.py`; the app reads it at startup.

## ⚙️ How it works

1. The app loads `tmdb_5000_movies.csv`.
2. It extracts each movie's genres, keywords, and overview.
3. These fields are combined into a text field called `tags`.
4. `CountVectorizer` converts the text into numerical feature vectors.
5. Cosine similarity measures how similar the movie vectors are.
6. When a user selects a movie, the app returns the five most similar titles (excluding the selected movie).
7. The app requests poster images from OMDb for the recommended titles.

**Note:** This is a content-based recommender. It uses movie metadata rather than user ratings or personal viewing history. Recommendations depend on the metadata available in the dataset.

## ✅ Requirements

- Python 3.10 or newer is recommended.
- Git (optional, but needed to push changes to GitHub).
- An internet connection for poster images and deployment.

## 🚀 Run locally

### 1. Clone the repository

```bash
git clone https://github.com/govindchaturvedi1995-svg/Movie-recommendation-system
cd movie-recommender-system
```

Alternatively, download the repository ZIP from GitHub and extract it.

### 2. Create and activate a virtual environment

**Windows PowerShell:**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt:

```bat
.venv\Scripts\activate.bat
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Configure the OMDb API key

The app uses OMDb to retrieve posters. Create an API key at [omdbapi.com](https://www.omdbapi.com/apikey.aspx).

For safer key management, update `streamlit_app.py` to read the key from an environment variable or Streamlit secrets instead of hardcoding it. For example, replace the hardcoded `API_KEY = ...` with:

```python
import os

API_KEY = os.getenv("OMDB_API_KEY", "")
```

Then set the key before starting the app.

**Windows PowerShell:**

```powershell
$env:OMDB_API_KEY="your_omdb_api_key"
```

**macOS / Linux:**

```bash
export OMDB_API_KEY="your_omdb_api_key"
```

You can also use Streamlit secrets. Add this to `.streamlit/secrets.toml` (do not commit this file):

```toml
OMDB_API_KEY = "your_omdb_api_key"
```

If using Streamlit secrets, read it in Python with:

```python
API_KEY = st.secrets.get("OMDB_API_KEY", "")
```

Choose the environment-variable approach or the Streamlit-secrets approach and keep the app code consistent with it. Never commit real API keys to a public repository. If a key has already been committed, revoke or rotate it.

### 5. Start the app

```bash
python -m streamlit run streamlit_app.py
```

Open the local URL shown in the terminal, usually [http://localhost:8501](http://localhost:8501).

## ☁️ Deploy on Streamlit Community Cloud

1. Push this project to your GitHub repository.
2. Open [Streamlit Community Cloud](https://share.streamlit.io/).
3. Sign in using GitHub and authorize access if prompted.
4. Select **Create app** (or **Deploy an app**).
5. Choose repository `4kayasitayashu/movie-recommender-system`, branch `main`, and main file `streamlit_app.py`.
6. Open the app's **Settings → Secrets** and add your key in TOML format:

   ```toml
   OMDB_API_KEY = "your_omdb_api_key"
   ```

7. Deploy the app. Streamlit installs packages from `requirements.txt`.
8. If deployment fails, open the app's logs and check the error message.

**Before deploying:** Make sure the code reads `OMDB_API_KEY` from `st.secrets` if you use Streamlit Cloud secrets. A secret configured in the dashboard will not replace a hardcoded key automatically.

## 🧪 Troubleshooting

- **`FileNotFoundError` for the CSV:** Ensure `tmdb_5000_movies.csv` is committed to the repository and sits beside `streamlit_app.py`.
- **`ModuleNotFoundError`:** Activate the virtual environment and run `pip install -r requirements.txt`.
- **Posters are missing:** Check your internet connection, API key, and OMDb request limits. Recommendations can still work even when posters are unavailable.
- **Streamlit command not found:** Run `python -m streamlit run streamlit_app.py`.
- **Git push rejected:** Fetch/pull the existing repository changes first rather than force-pushing; inspect the Git error before proceeding.

## 💡 Possible future enhancements

These are ideas for future versions and are **not all implemented yet**:

- Search movies by title instead of using only a dropdown.
- Show movie overview, release year, genres, and rating.
- Add filters for genre, language, or release year.
- Let users choose how many recommendations to display.
- Cache poster requests and similarity calculations to improve startup and response times.
- Add a fallback image and friendlier API error messages.
- Add user ratings, favourites, and watchlists.
- Compare collaborative filtering with the current content-based approach.
- Add automated tests and a continuous-integration workflow.
- Improve accessibility and mobile layout.

## 📌 Current limitations

- The app recommends movies from the included dataset only.
- It currently displays five recommendations.
- Recommendation quality depends on the genres, keywords, and overview fields in the dataset.
- Poster availability depends on OMDb and its API limits.
- The current implementation calculates the similarity matrix when the app starts, which may take time on limited hardware.

## 📄 Dataset and API notes

- The project uses the TMDB 5000 Movies dataset. Review the dataset's original source and terms before redistributing it.
- Movie posters are requested from OMDb. Refer to [OMDb API](https://www.omdbapi.com/) for its usage terms and limits.
- This is an educational/demo project and is not affiliated with TMDB or OMDb.

## 🤝 Contributing

Suggestions and pull requests are welcome. For a change:

1. Fork the repository.
2. Create a feature branch.
3. Make and test your changes.
4. Open a pull request describing the change.

## 📜 License

No license is included unless one is added to this repository. Add a license file before allowing others to reuse, modify, or redistribute the project under explicit terms.
