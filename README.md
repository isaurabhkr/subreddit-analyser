# subreddit-analyser
A set of Python notebooks to scrape and analyze subreddit posts. 

The Analysis is divided into three major steps:
1. Crawl Sub-Reddit data using the PushshiftAPI.
2. Preprocess the crawled data and perform feature-extraction.
3. Plot the data points and conclude from data.


## Preparation of Data-set:
- We have used the PushshiftAPI to crawl data.- The API has a get request with different query parameters and return JSON object containing the post information. </br>

- Sample URL:   https://api.pushshift.io/reddit/submission/search/?after=1577750400&subreddit=emacs&size=100&sort_type=created_utc&sort=asc&fields=author,author_fullname,created_utc,domain,full_link,is_crosspostable,link_flair_text,num_comments,num_crossposts,over_18,permalink,score,selftext,title,total_awards_received

- After an analysis of different entries that we received from the API. I have used fields author, author_fullname, created_utc, domain, full_link, is_crosspostable, link_flair_text, num_comments, num_crossposts, over_18, permalink,score, selftext, title, total_awards_received


## Data-set: 
- We have crawled and created data-set of subreddit posts from `r/emacs` and `r/vim`. The data-set represents the posts made on these subreddits by users from January 1st 2020 to March 31st 2020.
- The emacs-raw data-set is fairly small with 1353 rows which includes posts that are deleted. To make this analysis more comprehensive we have filtered out the deleted posts and then the resultant vim-filtered has 1255 rows, which indicates only 98 posts were deleted.
- The vim-raw data-set is also fairly small with 1136 rows which includes posts that are deleted. To make this analysis more comprehensive we have filtered out the deleted posts and then the resultant vim-filtered has 1132 rows, which indicates only 4 posts were deleted. It is significantly lower from the number of deleted posts from the /emacs subreddit.


## Feature Extraction:
- After careful analysis of the data that is crawled, We identified the most relevant features that can help us understand the pattern and behaviour of users posting in the subreddits:
- One of the important thing to understand about user engagement in any social media to know if their posts have a positive sentiment or negative sentiment.
- We calculated sentiment from the `title` of the post and the `content` of the post, and populated the feature table with post_sentiment and title_sentiment using the VADER `SentimentIntensityAnalyzer`.
- VADER (Valence Aware Dictionary and sEntiment Reasoner) is a lexicon and rule-based sentiment analysis tool that is specifically attuned to sentiments expressed in social media.
- The other information about social media is captured by `reddit_score` which is the `(total number of upvotes - total number of downvotes)`.- We also kept the author of the post along with the total number of comments on the post.
- The date of creation of post is also kept as a feature for us to analyse this data from a time-series perspective.


## Top 5 metrics in the feature CSV
- `date_created`: The date of creation of the post
- `author`: The author of the post. It is the username of the author
- `post_sentiment` : The sentiment of post: Positive, Negative or Neutral
- `reddit_score`: The Reddit score which is the total number of upvotes - total number of downvotes
- `num_comments`: The total number of comments on the post
-  We have also kept `post` and `title` columns to uniquely identify the post.


## Data Visualization and conclusion
- The analysis is captured in Python Notebooks present in `py-notebook` directory.
- The conclusions are summarized in the report file.
