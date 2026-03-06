# Netflix Data Analysis Project

# Import required libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv("/content/netflix_titles.csv")

# Display first 5 rows
print("First 5 rows of dataset:")
print(df.head())

# Dataset information
print("\nDataset Information:")
print(df.info())

# Check missing values
print("\nMissing Values:")
print(df.isnull().sum())

# Movies vs TV Shows count
plt.figure(figsize=(6,4))
sns.countplot(x='type', data=df)
plt.title("Movies vs TV Shows on Netflix")
plt.xlabel("Type")
plt.ylabel("Count")
plt.show()

# Top 10 countries producing Netflix content
plt.figure(figsize=(8,5))
top_countries = df['country'].value_counts().head(10)
top_countries.plot(kind='bar')
plt.title("Top 10 Countries Producing Netflix Content")
plt.xlabel("Country")
plt.ylabel("Number of Titles")
plt.show()

# Content released per year
plt.figure(figsize=(8,5))
df['release_year'].value_counts().sort_index().plot()
plt.title("Netflix Content Released Per Year")
plt.xlabel("Year")
plt.ylabel("Number of Titles")
plt.show()

# Most popular genres
genres = df['listed_in'].str.split(',', expand=True).stack()
top_genres = genres.value_counts().head(10)

plt.figure(figsize=(8,5))
top_genres.plot(kind='bar')
plt.title("Top 10 Netflix Genres")
plt.xlabel("Genre")
plt.ylabel("Count")
plt.show()

# Ratings distribution
plt.figure(figsize=(8,6))
sns.countplot(y='rating', data=df, order=df['rating'].value_counts().index)
plt.title("Distribution of Ratings on Netflix")
plt.xlabel("Count")
plt.ylabel("Rating")
plt.show()

print("\nAnalysis Completed Successfully!")
