# Claude Prompt for Midterm

# 1. Project definition and relevance.
Clearly describe the problem or opportunity addressed by the project and explain its relevance from a business, organizational, or decision-making perspective. The problem should be clearly motivated and analytically meaningful.

### Ryan's Notes
> The ideas we had here were:
> 1. Predict the popularity of an artists next album based on their past success
> 2. Descriptive: Using filters, recommend a song or artist 
> 3. Descriptive: Popularity of a song based on a key or time signature (is 4/4 time more popular than 7/8 or do people prefer the key of Em over G major for example) - or maybe, which audio parameters are the best indicator of a song's popularity (key, time signature, danceability, acousticness, etc.)
> 4. I asked Claude for some ideas as well, which are below
> 5. I think once we nail down 3 or 4 of these, we can generate our project definition and relevance fairly easily. Again, GenAI can help us here with the wording for the slides prompt.
#### Claude assisted ideas
##### Descriptive Analytics

- **Genre profiles**: average danceability, energy, valence, tempo, etc. by `track_genre` — which genres are the happiest, most energetic, most acoustic
- **Popularity distribution**: how popularity is distributed overall and within genres; are a few genres dominating the "popular" tail
- **Explicit content trends**: rate of explicit tracks by genre, and whether explicit tracks trend more/less popular
- **Duration patterns**: typical song length by genre or era, outlier detection for unusually short/long tracks
- **Key/mode frequency**: which keys and major/minor splits are most common, and whether that varies by genre
- **Time signature breakdown**: how dominant 4/4 is vs. others, and which genres deviate
- **Correlation matrix**: relationships among energy, loudness, valence, danceability, acousticness (e.g., energy and loudness are almost always tightly correlated)
- **Artist-level rollups**: which artists have the most tracks, highest average popularity, or most genre diversity

##### Predictive Analytics

- **Popularity prediction**: regression or gradient boosting (XGBoost/LightGBM) using audio features + genre + explicit + duration to predict `popularity`; useful for feature importance (what actually drives popularity)
- **Genre classification**: multi-class classifier using only audio features (danceability, energy, valence, tempo, etc.) — see how well genre can be inferred from "sound" alone, and which genres get confused with each other
- **Explicit content classifier**: predict `explicit` from lyrics-adjacent features like speechiness, or see if it's predictable at all from audio features (probably not — good null-result exercise)
- **"Danceable hit" classifier**: binary classification for whether a track crosses a popularity threshold, useful for a "will this song be a hit" style model
- **Valence/mood prediction**: predict valence from other features to explore what makes a song "sound happy"

##### Unsupervised / Exploratory Analytics

- **Clustering tracks** (k-means, DBSCAN, or Gaussian mixture) on standardized audio features to discover natural "sound clusters" that may cut across labeled genres — interesting to see if clusters align with or defy `track_genre`
- **Genre similarity map**: aggregate audio features by genre, then cluster or use hierarchical clustering to build a genre similarity dendrogram
- **Dimensionality reduction**: PCA, t-SNE, or UMAP on the audio features to visualize the overall "sound space" of the dataset, colored by genre or popularity — often reveals interesting structure like a mood/energy axis
- **Anomaly detection**: isolation forest or local outlier factor to find tracks that are audio-feature outliers within their genre (e.g., a "metal" track with very low energy)
- **Association rules**: look for feature combinations that frequently co-occur (e.g., high liveness + high energy + specific genre)
- **Topic-style clustering on artists**: cluster artists based on the aggregated feature profile of their catalog, to find "sonic neighbors" across genre labels

##### A Few Specific, Punchy Questions to Frame the Analysis

- Does danceability actually predict popularity, or is that a myth?
- Is there a "loudness war" visible — has energy/loudness crept up over time or by genre?
- Do explicit tracks get systematically higher or lower popularity?
- Which genres are most "danceable but sad" (high danceability, low valence) — an interesting mismatch to explore?
- How distinguishable are genres purely from audio features, without knowing the label?


### Grace's Notes

> my faorite central idea: **predictive regression — which audio characteristics best predict a track's popularity?**
>
> Using danceability, energy, loudness, valence, tempo, acousticness, speechiness, explicit, and duration as predictors, with genre as a possible categorical control. This gives us a specific & measurable question as our main deliverable
>
> I would add ~3 mini-projects that use the same feature data to keep consistency with the main deliverable. here's a couple ideas:
> 1. **Correlation/descriptive foundation**  correlation matrix across the core audio features (energy, loudness, valence, danceability, acousticness), used to justify our feature choices in the regression (e.g., if energy and loudness are tightly correlated, we may drop one or combine them)
> 2. **Unsupervised clustering**  cluster tracks by audio features and compare the clusters to Spotify's own `track_genre` labels. Question: does the natural structure in the data match Spotify's genre taxonomy, or reveal something different?
> 3. **Myth-busting validation**  take 2-3 fun sub-questions (does danceability actually predict popularity? are explicit tracks more or less popular?) and answer them directly using the regression's feature importance, rather than as standalone stats
>
>some data callouts (114,000 rows, 20 columns, 114 genres):
> - **24,259 duplicate `track_id` rows** — same tracks repeat under multiple genres. We'll need to choose which to keep or aggregate 
> - Popularity is **skewed low** — median 35, mean 33, full range 0-100. Worth deciding early whether we model raw popularity (regression) or bucket into tiers (classification), since this affects how we frame results.
> - Only 3 missing values total, but duration has outliers


# 2. Project Goal and Research Questions.
Clearly state the **goal of the project** and define one or more **research questions** that will guide the analysis. Research questions should be specific, measurable, and analytically actionable.
### Ryan's Notes
> Similar to the first item, once we nail down the 3-4 items we really like, this should be straightforward to do with GenAI assist.


# 3. Intended analytics approach (descriptive, predictive, or unsupervised).
Specify how the methodological focus selected will contribute to responding to the research question stated.


# 4. Dataset selection and justification.
Identify the dataset selected for the project and explain **why this dataset is appropriate** for addressing the defined problem. The justification should consider data relevance, structure, variables available, and analytical feasibility.

[Spotify Tracks Dataset | Kaggle](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)

# 5. Data Preparation.
1. **Data Exploration.** Provide a preliminary exploration of the dataset, including:
        - Key variables and their types.
        - Initial distributions, relationships, and patterns.
        - Data quality issues such as missing values, outliers, or inconsistencies.
2. **Data Wrangling and Correction** (if required). Describe the data cleaning and preparation steps performed, including handling missing values, addressing outliers, correcting inconsistencies, and applying transformations as needed. All decisions must be explained and justified.
# 6.  Execution Plan.
Present a clear plan outlining **how the project will be completed** over the remaining weeks of the semester. The plan should identify key steps, milestones, and analytical activities, demonstrating that the project is feasible and well-organized.


# 7. Conclusions.
Conclude the presentation with a concise summary highlighting:
    - Project readiness.
    - Key risks or challenges.
    - Next steps toward final delivery.
    - Personal learnings.



# 8. Prompt for Gemini
Create a 10-slide presentation on (insert the business problems here - parts 1 -3). 

**Audience**: The audience for this slide deck is executives at a recording studio and we are consultants helping them understand the music industry landscape using data collected from Spotify. 

**Goal**: Use the business value here too

**Tone**: Data-driven and direct, no fluff

**Structure the slides as follows**: 
1. Title slide — Music Industry Trends 2026 (Presenters Grace Bosma, Jered Ross, and Ryan Brock)
2. Executive summary — the single most important takeaway, stated as a conclusion, not a topic 
3. . [List the specific points/sections you want covered, in order] 
4. Recommendation(s) — clear, specific, actionable 
5. Next steps / appendix pointer 

**For each slide, give me**: 
- A headline that states the takeaway (not just a label like "Analysis" — something like "Running Shoes Drive 3x More Returns Than Any Other Category") 
- 3-5 supporting bullets, each one line, no sub-bullets 
- A note on what visual would work best (chart type, table, or image) and what data it should show 

**Constraints**: - No slide should have more than ~40 words of text - Avoid generic stock-photo language or filler phrases - provide clean, professional, visuals based on the content of each slide - Keep the whole deck tight enough to present in 20 minutes

