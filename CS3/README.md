DS4002 Case Study: Exploring Cultural Connections in Music Lyrics
Spring 2025 -- Lauren Turner
This repository contains information, data, and scripts based on Project 1 of DS4002, which focused on word-based data. You are tasked to use a TF-IDF (Term Frequency - Inverse Document Frequency) model to explore polular music lyrics.

This repository is organized as follows:
image

Reproducing Results
Gathering Data
In order to reproduce our results, find some top charts playlists from the cities you would like to analyze (can be from Apple Music, Spotify, Amazon Music, SoundCloud, etc.). Enter the song name and artist into a .txt file in the format ("song_name", "artist") with each song separated by commas (see DATA/sample_song_list). Register for the Genius API: https://docs.genius.com/#/getting-started-h1 ; save your access token. Open SCRIPT/1_Lyric_Scraper.py and input each song list and run to create a .csv file with all of the lyrics data.

EDA
Use the general data to complete exploratory data analysis. This can be creating a word cloud, analyzing the most popular genres/artists, or creating different charts. See SCRIPT/2_EDA.ipynb for examples.

Analysis: TF-IDF
Load in each cities' lyrics as a csv. Convert each cities' CSV to a text string. Create a list called "cities". Each item in "cities" should be the name of a given city. Create the list of "documents" to be analyzed. You can call this list "corpus". Each item in "corpus" should be a text string containing all of the lyrics for a given city. Filter certain words from the corpus for the analysis. To filter, use stop_words="english" as an argument to the TfidfVectorizer() function. This argument is a built-in list of English stop words that will be removed from the TF-IDF analysis. Stop words are common words (e.g., "the", "and", "is"). Additionally, manually remove probelmatic words. To do this, include another list of custom stop words like "lyrics" and "chorus" that were appearing within our analysis. Remove the custom list of words from the corpus. We chose to remove stop words because we found that stop words such as "is", "the" and "and" were appearing in almost all of the top 10 lists, taking away from our analysis. After removing the stop words we used the TfidfVectorizer() function. Save the output as "vectorizer". Apply the fit_transform() to the corpus, as shown below.

vectorizer = TfidfVectorizer(stop_words="english") X = vectorizer.fit_transform(corpus)

Convert the output to a dataframe. tfidf_df = pd.DataFrame(X.toarray(), index=cities, columns=vectorizer.get_feature_names_out())

Use a "for" loop to print the top ten highest TF-IDF values and words for each of the cities. Compare and analyze the results.
