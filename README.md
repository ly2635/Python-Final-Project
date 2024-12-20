# Python-Final-Project

**Analyzing Reddit Discussions on the Relationship Between Interest Rates and Housing Prices in the U.S.**

**Introduction**  
The relationship between Federal Reserve interest rate decisions and housing price trends has long been a topic of public and academic interest. Changes in interest rates can influence mortgage costs, housing demand, and broader market stability, making this an essential issue for prospective homeowners, investors, and policymakers alike. Platforms like Reddit, where individuals from diverse backgrounds engage in detailed discussions, provide a unique opportunity to understand how these policies affect public sentiment and financial decision-making.

This project focuses on analyzing Reddit discussions, particularly from the *r/MiddleClassFinance* subreddit, to uncover prevailing attitudes toward the impact of interest rate changes on housing prices. By examining posts and comments from this community, this research aims to identify key themes, arguments, and emotional tones that shape public understanding of this critical economic issue.

---

**Research Questions**  
1. What are the prevailing attitudes among Reddit users about the relationship between interest rates and housing prices?  
2. How do perspectives differ among various demographic groups, such as homeowners, prospective buyers, and financial advisors?  
3. What recurring themes or concerns dominate discussions about interest rate changes and their impact on housing affordability?  
4. How do media narratives and recent economic events shape the tone and content of these discussions?

---

**Literature Review**  
The academic literature highlights the nuanced impact of interest rates on the housing market. Studies such as Glaeser et al. (2012) explore how low interest rates can spur housing demand, while others like Himmelberg et al. (2005) emphasize the role of housing supply and broader market conditions. Reddit discussions provide a complementary perspective, revealing how individuals interpret these economic theories in real-world contexts. This project builds on existing research by leveraging social media data to analyze how public sentiment aligns—or diverges—from academic and policy-driven narratives.

---

**Data Sources**  
- **Primary Source**: Comments and posts from the *r/MiddleClassFinance* subreddit, particularly the thread: "[If interest rates go down, do housing prices go up?](https://www.reddit.com/r/MiddleClassFinance/comments/1cc3r5j/if_interest_rates_go_down_do_housing_prices_go_up/)"  
- **Supporting Literature**:  
  - Glaeser, E. L., et al. (2012). Housing supply and demand. *Journal of Economic Perspectives*.  
  - Himmelberg, C., et al. (2005). Assessing high house prices: Bubbles, fundamentals, and misperceptions. *Journal of Economic Perspectives*.  

---

**Hypothesis**  
This project hypothesizes that Reddit users generally perceive interest rate changes as a significant factor influencing housing prices, but views will likely diverge based on individual circumstances. While some may emphasize affordability challenges, others may focus on investment opportunities or the broader economic implications.

---

**Methodology**  
1. **Data Collection**: Using the PRAW API, posts and comments from the specified Reddit thread will be collected. Focus will be placed on extracting meaningful text data, including user comments and post metadata.  
2. **Sentiment Analysis**: Tools like NLTK and VADER will be used to analyze the emotional tone of comments and classify them as positive, negative, or neutral.  
3. **Thematic Analysis**: Text analysis methods, such as keyword extraction and topic modeling (using tools like gensim or spaCy), will identify dominant themes and concerns.  
4. **Comparison**: Findings from Reddit discussions will be compared with academic insights and broader public opinion trends to assess alignment or divergence.

---

**Importance**  
This research is significant because it bridges the gap between public discourse and academic theories on housing market dynamics. By focusing on Reddit discussions, this study offers insights into how individuals interpret and react to interest rate changes, providing valuable context for policymakers, financial educators, and researchers. The findings can also inform outreach strategies, helping stakeholders address misconceptions and foster informed decision-making.

---

**Expected Outcomes**  
1. A nuanced understanding of public sentiment toward the relationship between interest rates and housing prices.  
2. Identification of key themes and arguments prevalent in Reddit discussions.  
3. Practical recommendations for policymakers and educators to address public concerns and enhance financial literacy.



# post 1 analysis
```python 
import asyncpraw
import asyncio
```

# Configure Reddit API
```async def get_post_details(post_url):
    reddit = asyncpraw.Reddit(
        client_id="LCe8jnL_D8Z5ZKKbwjt__Q",
        client_secret="V8D21qPDX2WYYlKI94z2SAoZzywAYQ",
        user_agent="MyRedditApp/1.0 by u/OkNothing5723",
    )
```

    try:
        submission = await reddit.submission(url=post_url)  # Await for asyncpraw submission
        post_data = {
            "Title": submission.title,
            "Author": submission.author.name if submission.author else "N/A",
            "Score": submission.score,
            "Comments_Count": submission.num_comments,
            "URL": submission.url,
            "Body": submission.selftext,
        }
        print("Post Details:")
        print(post_data)
        return post_data
    except Exception as e:
        print(f"Error: {e}")
        return None

# Set the post URL
```python
post_url = "https://www.reddit.com/r/MiddleClassFinance/comments/1cc3r5j/if_interest_rates_go_down_do_housing_prices_go_up/"
```

# Run the asynchronous function
```
import asyncio
async def main():
    post_details = await get_post_details(post_url)
    if post_details:
        print("Processing post details...")
    else:
        print("Could not retrieve post details.")

asyncio.run(main())
```
```
post_data = {
    "Title": submission.title,
    "Author": submission.author.name if submission.author else "N/A",
    "Score": submission.score,
    "Comments": submission.num_comments,
    "Body": submission.selftext
}
```
```
async def get_post_details(post_url):
    # Initialize asyncpraw Reddit instance
    async with asyncpraw.Reddit(
        client_id="LCe8jnL_D8Z5ZKKbwjt__Q",
        client_secret="V8D21qPDX2WYYlKI94z2SAoZzywAYQ",
        user_agent="MyRedditApp/1.0 by u/OkNothing5723",
    ) as reddit:  # Use async with to ensure proper cleanup
        try:
            submission = await reddit.submission(url=post_url)  # Await the submission
            post_data = {
                "Title": submission.title,
                "Author": submission.author.name if submission.author else "N/A",
                "Score": submission.score,
                "Comments": submission.num_comments,
                "Body": submission.selftext
            }
            print("Post Details:")
            print(post_data)
            return post_data  # Return the submission data
        except Exception as e:
            print(f"Error: {e}")
            return None
        finally:
            await reddit.close()
            ```
``` python
import pandas as pd

async def main():
    post_url = "https://www.reddit.com/r/MiddleClassFinance/comments/1cc3r5j/if_interest_rates_go_down_do_housing_prices_go_up/"
    post_details = await get_post_details(post_url)
    if post_details:
        # Convert to DataFrame
        df = pd.DataFrame([post_details])
        # Save to CSV
        df.to_csv("reddit_post_details.csv", index=False)
        print("Post details saved to CSV.")
    else:
        print("Could not retrieve post details.")
asyncio.run(main())
```
```
df = pd.read_csv("reddit_post_details.csv")
print(df.head())
```


