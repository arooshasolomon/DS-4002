# DS4002 Case Study Exploring the nuance of music lyrics and culture 
DS4002 Spring 2025 Project Group LAM

Aroosha Solomon
## Repository Contents
This repository includes information, datasets, and scripts from Project 1 of DS4002, which centers on word-based data analysis. Your task is to apply a TF-IDF (Term Frequency–Inverse Document Frequency) model to explore popular music lyrics.

## Software and Platform
For this project, we used Google Colab and Jupyter Notebook, working with both Python and RScript. The data was sourced from Apple Music's city charts, and lyrics were obtained via the Genius API. We utilized several additional packages, including: matplotlib, pandas, requests, BeautifulSoup, time, html, tm, wordcloud, RColorBrewer, sklearn, TfidfVectorizer, os, and re. Development was conducted on macOS.


## Documentation Map
![image](https://github.com/user-attachments/assets/62a363dd-6b83-42c2-b828-fe518d11283d)


## Reproducing Results
### Gathering Data
To reproduce our results, begin by collecting top chart playlists from the cities you want to analyze.These can come from platforms like Apple Music, Spotify, Amazon Music, or SoundCloud. Create a .txt file containing the song titles and artists in the following format:
("song_name", "artist"), with each entry separated by commas (refer to DATA/sample_song_list for an example).
Next, register for access to the Genius API at https://docs.genius.com/#/getting-started-h1 and save your access token.
Then, open SCRIPT/1.lyric_scraper_script.py, input your song list, and run the script to generate a .csv file containing the lyrics data.


### EDA
Use the general data to complete exploratory data analysis. This can be creating a word cloud, analyzing the most popular genres/artists, or creating different charts. See SCRIPT/2.1EDA.ipynb and SCRIPT/2.2EDA.R for examples.
### Analysis: TF-IDF
Begin by loading each city’s lyrics data from its respective CSV file. Convert each CSV into a single text string.
Create a list called cities, where each item is the name of a city. Then, build a corresponding list called corpus, where each item is a text string containing all lyrics for that city. To prepare the data for analysis, filter out unnecessary words from the corpus. Use the argument stop_words="english" with the TfidfVectorizer() function to automatically remove common English stop words such as "the", "and", and "is". Additionally, define a custom list of words to exclude—such as "lyrics" and "chorus"—which may appear frequently but do not add meaningful value. Manually remove these custom stop words from the corpus. We chose to remove stop words because many appeared consistently across top results, diluting the distinctiveness of each city’s lyrical content.After cleaning the text, initialize the TfidfVectorizer() and save it as vectorizer. Then, apply the .fit_transform() method to the corpus to generate the TF-IDF matrix.

vectorizer = TfidfVectorizer(stop_words="english")
X = vectorizer.fit_transform(corpus)

Convert the output to a dataframe.
tfidf_df = pd.DataFrame(X.toarray(), index=cities, columns=vectorizer.get_feature_names_out())

Use a "for" loop to print the top ten highest TF-IDF values and words for each of the cities. Compare and analyze the results.
