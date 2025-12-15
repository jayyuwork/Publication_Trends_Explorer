# Publication Trends Explorer
The project developed and implemented a Machine Learning algorithm to tackle the challenge of identifying emerging, high-impact research trends within the academic literature, specifically focusing on the Machine Learning domain.

## Methodology
The workflow begins with data acquisition from arXiv publications and then leverages Semantic Scholar citations as the ultimate measure of influence. To precisely filter down to truly impactful papers, I implemented a robust selection process: I used Z-score analysis on the citation counts to quantify and normalize the publication's impact relative to its peers within the same field and time window.

## Implementation and Results
For the chosen publications, I employed a modern NLP approach. I utilized a pre-trained BERT model to encode the publication abstracts, generating rich, contextual vector representations. I then clustered these encoded vectors to identify distinct topics. To make these abstract clusters human-interpretable, I applied TF-IDF (Term Frequency-Inverse Document Frequency) to extract the most descriptive topic words, which were then used for visualization and trend analysis. 
