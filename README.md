<H3>ENTER YOUR NAME: SWETHA S</H3>
<H3>ENTER YOUR REGISTER NO.: 212222230155</H3>
<H3>DATE: 30/10/2025</H3>

<H1 Align="center">Project Based Experiment</H1>

<H3>Objective:</H3>
<p>
To perform sentiment analysis on Facebook post data using NLTK’s VADER SentimentIntensityAnalyzer, 
and to filter and display only the negative feedback posts from the dataset.
</p>

<H3>Program:</H3>

<pre>
from nltk.sentiment.vader import SentimentIntensityAnalyzer
import pandas as pd
import nltk
from google.colab import files

# Upload file
uploaded = files.upload()   # Choose fb_sentiment.xlsx from your computer

# Download VADER lexicon
nltk.download('vader_lexicon')

# Load Excel file
file = "fb_sentiment.xlsx"
xl = pd.ExcelFile(file)

# Read the first sheet
dfs = xl.parse(xl.sheet_names[0])

# Use the correct text column
posts = list(dfs['FBPost'])

# Initialize Sentiment Analyzer
sid = SentimentIntensityAnalyzer()

# Analyze sentiment
results = []
for post in posts:
    scores = sid.polarity_scores(str(post))
    compound = scores['compound']
    if compound >= 0.05:
        sentiment = 'Positive'
    elif compound <= -0.05:
        sentiment = 'Negative'
    else:
        sentiment = 'Neutral'
    results.append({'Post': post, 'Compound': compound, 'Sentiment': sentiment})

sentiment_df = pd.DataFrame(results)

# Filter only negative feedback
negative_feedback = sentiment_df[sentiment_df['Sentiment'] == 'Negative']

# Display results
print("\n🛑 Negative Feedback Posts:")
print(negative_feedback[['Post', 'Compound']])

# Save results
negative_feedback.to_excel("NegativeFeedbackOnly.xlsx", index=False)
print("\nNegative feedback saved to NegativeFeedbackOnly.xlsx ✅")
</pre>

<H3>Output:</H3>
<img width="693" height="500" alt="image" src="https://github.com/user-attachments/assets/b4468b29-a1dc-44c7-a22e-0aeabfefb8c7" />


<H3>Inference:</H3>
<p>
From this project, I learned how to use the <b>NLTK VADER sentiment analysis</b> tool to analyze 
text data and classify it into positive, negative, and neutral sentiments. I also gained 
hands-on experience working with Excel data using <b>Pandas</b>, performing data filtering, 
and saving results programmatically. This experiment helped me understand how text mining and 
sentiment analysis can be applied to real-world social media data.
</p>
