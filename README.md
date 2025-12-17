# Publication Trends Explorer

This project leverages Machine Learning and Natural Language Processing (NLP) to identify and track emerging, high-impact research trends within the academic literature (specifically cs.LG, cs.AI, and stat.ML).

## Project Overview

Academic publishing is growing at an exponential rate, making it difficult to track which sub-fields are gaining genuine traction. This project solves this by:

- **Quantifying Influence**: Using Z-score normalization to isolate high-impact papers relative to their peers.
- **Semantic Mapping**: Leveraging Transformer-based embeddings to group research into distinct, high-density topics.
- **Noise Reduction**: Using density-based clustering to ensure only cohesive research trends are identified.

## Methodology

### 1. Data Acquisition & Normalization

The dataset comprises ~500,000 abstracts from the arXiv dataset, enriched with Semantic Scholar citation metadata. To identify "impact," raw citation counts are insufficient due to temporal bias (older papers have more time to gather citations). I implemented a **Sliding Window Z-Score**:

- **Formula**: Z = (x - μ) / σ
- **Logic**: Papers are compared only to others in the same field and time window. A Z-score > 0 indicates a paper is performing above the mean for its cohort.

### 2. Semantic Encoding (all-MiniLM-L6-v2)

For text vectorization, I utilized the `all-MiniLM-L6-v2` model. This choice provides an ideal balance between performance and speed:

- **Vector Space**: Maps abstracts into a 384-dimensional dense vector space, capturing deep semantic relationships beyond simple keyword overlap.
- **Efficiency**: Optimized for "word pieces" (up to 256 tokens), making it perfectly suited for academic abstracts.
- **Semantic Search**: Unlike traditional BoW models, this allows the system to recognize that "Neural Networks" and "Deep Learning" are semantically adjacent in the vector space.

### 3. Density-Based Clustering (HDBSCAN)

Unlike K-Means, which forces every point into a cluster, HDBSCAN was chosen for its robustness:

- **Outlier Detection**: Points that don't belong to a dense trend are labeled as "noise."
- **Shape Agnostic**: It can find clusters of any shape, which is vital for high-dimensional vector space.
- **Automatic K**: No need to pre-define the number of topics.

### 4. Topic Words

To make these abstract clusters human-interpretable, I applied TF-IDF (Term Frequency-Inverse Document Frequency) to extract the most descriptive topic words, which were then used for visualization and trend analysis.

## Results

This research was presented at the 2020 Rice University Data Science Conference.

- **Poster Session**: [Data Science Conference at Rice University](https://2020ricedsconference.rice.edu/poster-session/)
- **Data Source**: [Kaggle ArXiv Dataset](https://www.kaggle.com/datasets/Cornell-University/arxiv/)
