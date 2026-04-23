# 🐦 Twitter Advanced Scraper 

<div align="center">

![Python Version](https://img.shields.io/badge/python-3.7%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-success)
![Contributions](https://img.shields.io/badge/contributions-welcome-brightgreen)

*A powerful, easy-to-use Python tool for extracting high-engagement tweets from Twitter/X with advanced filtering capabilities*

[Features](#-features) • [Installation](#-installation) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [Examples](#-examples)

</div>

---

## 📋 Overview

Twitter Advanced Scraper is a robust Python library that enables you to extract tweets from Twitter/X based on search queries or user profiles. Filter results by engagement metrics (likes, comments, views) to find the most impactful content. Perfect for social media analysis, market research, trend monitoring, and content curation.

### Why Use This Scraper?

- ✅ **Engagement Filtering** - Find tweets with minimum likes, comments, and views
- ✅ **Dual Search Modes** - Search by keywords or specific user profiles  
- ✅ **Rich Data Export** - Get complete tweet metadata in JSON format
- ✅ **Smart Pagination** - Automatically fetch multiple pages of results
- ✅ **Cookie Rotation** - Built-in cookie management for reliability
- ✅ **Easy Integration** - Simple API that works out of the box

---

## 🚀 Features

| Feature | Description |
|---------|-------------|
| **Search Timeline** | Search Twitter for any keyword or hashtag |
| **Profile Scraping** | Extract tweets from specific user profiles |
| **Engagement Filters** | Set minimum thresholds for likes, comments, and views |
| **Flexible Sorting** | Choose between "Top", "Latest", or "People" results |
| **Auto-Pagination** | Fetch multiple pages automatically |
| **JSON Export** | Save results in clean, structured JSON format |
| **Error Handling** | Built-in retry logic and error management |

---

## 🛠️ Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/twitter-advanced-scraper.git
cd twitter-advanced-scraper
```

### Step 2: Install Dependencies

```bash
pip install requests mahdix
```

### Step 3: Configure Cookies

Add your Twitter cookies to the `cookies_list` in `main.py`:

```python
cookies_list = [
    'your_cookie_string_here'
]
```

> **💡 Tip:** You can add multiple cookies for rotation and reliability.

---

## ⚡ Quick Start

### Basic Example - Search by Keyword

```python
from main import main

# Search for tweets about "Python programming" with high engagement
results = main(
    search_topi=['Python programming'],
    count=20,
    reaction_count=100,      # Minimum likes
    views_count=1000,        # Minimum views
    comment_count=10,        # Minimum comments
    mathods='TwitterSearchTimeline',
    number_lop=5
)

print(results)
```

### Basic Example - Scrape User Profile

```python
from main import main

# Get tweets from Elon Musk's profile
results = main(
    search_topi=['elonmusk'],
    count=15,
    reaction_count=500,
    views_count=10000,
    comment_count=50,
    mathods='profile_search',
    number_lop=3
)

print(results)
```

---

## 📖 Documentation

### Main Function Parameters

```python
main(search_topi, count, reaction_count, views_count, comment_count, mathods, number_lop)
```

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `search_topi` | list | Search queries or usernames | `['AI', 'ChatGPT']` or `['elonmusk']` |
| `count` | int | Maximum tweets to retrieve | `50` |
| `reaction_count` | int | Minimum likes required | `100` |
| `views_count` | int | Minimum views required | `1000` |
| `comment_count` | int | Minimum comments required | `10` |
| `mathods` | str | Search method: `'TwitterSearchTimeline'` or `'profile_search'` | `'TwitterSearchTimeline'` |
| `number_lop` | int | Number of pagination loops | `5` |

### Search Methods

#### 1. TwitterSearchTimeline

Search Twitter by keywords, hashtags, or phrases.

**When to use:** Finding trending topics, tracking hashtags, discovering viral content

```python
results = main(
    search_topi=['#AI', 'machine learning'],
    count=30,
    reaction_count=200,
    views_count=5000,
    comment_count=20,
    mathods='TwitterSearchTimeline'
)
```

**Available Products:**
- `'Top'` - Most relevant and engaging tweets
- `'Latest'` - Most recent tweets
- `'People'` - Tweets from people you might follow

#### 2. Profile Search

Extract tweets from specific user profiles.

**When to use:** Analyzing influencer content, monitoring brand accounts, tracking competitors

```python
results = main(
    search_topi=['jack', 'naval'],
    count=25,
    reaction_count=300,
    views_count=10000,
    comment_count=30,
    mathods='profile_search'
)
```

---

## 💡 Examples

### Example 1: Track Crypto Trends

```python
# Find highly engaged cryptocurrency tweets
crypto_tweets = main(
    search_topi=['#Bitcoin', '#Ethereum', '#Crypto'],
    count=100,
    reaction_count=1000,
    views_count=50000,
    comment_count=100,
    mathods='TwitterSearchTimeline',
    number_lop=10
)

# Save to file
import json
with open('crypto_trends.json', 'w', encoding='utf-8') as f:
    json.dump(crypto_tweets, f, ensure_ascii=False, indent=4)
```

### Example 2: Analyze Tech Influencers

```python
# Compare content from tech leaders
influencers = main(
    search_topi=['sama', 'pmarca', 'naval', 'elonmusk'],
    count=50,
    reaction_count=500,
    views_count=100000,
    comment_count=50,
    mathods='profile_search',
    number_lop=5
)

# Process results
for user_data in influencers:
    username = user_data['keyword']
    tweet_count = len(user_data['tweets'])
    print(f"{username}: {tweet_count} high-engagement tweets found")
```

### Example 3: Monitor Breaking News

```python
# Track news as it happens
news_tweets = main(
    search_topi=['breaking news', 'latest update'],
    count=30,
    reaction_count=50,
    views_count=10000,
    comment_count=5,
    mathods='TwitterSearchTimeline',
    number_lop=3
)

# Filter by recency
from datetime import datetime
recent_tweets = [
    tweet for user in news_tweets 
    for tweet in user['tweets']
    if 'Jan 2026' in tweet['date_of_post']
]
```

---

## 📊 Output Format

The scraper returns data in this structure:

```json
[
    {
        "type": "profile",
        "keyword": "elonmusk",
        "tweets": [
            {
                "post_id": "1234567890123456789",
                "post_url": "https://x.com/elonmusk/status/1234567890123456789",
                "date_of_post": "Mon Jan 20 15:30:00 +0000 2026",
                "tweet": "Full tweet text here...",
                "likes": 15000,
                "comments": 850,
                "views": "2500000"
            }
        ]
    }
]
```

### Field Descriptions

| Field | Description |
|-------|-------------|
| `type` | Type of search performed (`"profile"` or `"search"`) |
| `keyword` | Search query or username used |
| `post_id` | Unique Twitter post ID |
| `post_url` | Direct URL to the tweet |
| `date_of_post` | Timestamp when tweet was posted |
| `tweet` | Full text content of the tweet |
| `likes` | Number of likes (favorites) |
| `comments` | Number of replies |
| `views` | Number of views (impressions) |

---

## 🎯 Use Cases

### Social Media Marketing
- Identify viral content in your niche
- Track competitor engagement strategies
- Find influencers for partnerships

### Market Research
- Analyze consumer sentiment
- Track brand mentions and perception
- Monitor industry trends and discussions

### Content Curation
- Discover trending topics for your audience
- Find high-quality content to share
- Build content calendars based on engagement data

### Academic Research
- Study social media patterns and behaviors
- Analyze public discourse on topics
- Collect data for sentiment analysis

### Journalism & News
- Monitor breaking stories in real-time
- Track public reactions to events
- Find eyewitness accounts and sources

---

## ⚙️ Advanced Configuration

### Custom Headers

Modify request headers in the `TwitterSearchTimeline` class:

```python
self.headers = {
    'authorization': 'Bearer YOUR_BEARER_TOKEN',
    'x-csrf-token': 'YOUR_CSRF_TOKEN',
    # ... other headers
}
```

### Cookie Management

Add multiple cookies for better reliability:

```python
cookies_list = [
    'cookie_1',
    'cookie_2',
    'cookie_3'
]
```

The scraper automatically rotates between cookies to distribute requests.

### Pagination Control

Adjust the number of loops for deeper searches:

```python
# Shallow search (faster)
results = main(..., number_lop=2)

# Deep search (more results)
results = main(..., number_lop=15)
```

---

## 🔧 Troubleshooting

### Common Issues

**Issue:** "Rate limit exceeded"
- **Solution:** Add more cookies or reduce `number_lop` parameter

**Issue:** "No results found"
- **Solution:** Lower your engagement thresholds (reaction_count, views_count, comment_count)

**Issue:** "Invalid cookie"
- **Solution:** Update your cookies from a fresh Twitter session

**Issue:** "Connection timeout"
- **Solution:** Check your internet connection or add proxy support

### Getting Fresh Cookies

1. Log into Twitter/X in your browser
2. Open Developer Tools (F12)
3. Go to Application → Cookies → https://x.com
4. Copy the entire cookie string
5. Paste into `cookies_list` in main.py

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Contribution Ideas
- Add support for more search filters
- Implement proxy rotation
- Add data visualization features
- Improve error handling
- Add unit tests
- Create a web interface

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ⚠️ Disclaimer

This tool is for educational and research purposes only. Please ensure you comply with Twitter's Terms of Service and API usage policies. The developers are not responsible for any misuse of this software.

**Important Notes:**
- Respect rate limits to avoid account restrictions
- Use cookies from your own accounts only
- Don't use for spam or harassment
- Be mindful of privacy and data protection laws

---
<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/33c4c1e0-2dab-44d7-b371-908507580fe5" />



## 💼 Contact Me for Paid Projects

Have a project in mind or need expert help?  
I'm available for **freelance work and paid collaborations**.

### 📬 Get in Touch

- 📧 **Email**: [shuvobbhh@gmail.com](mailto:shuvobbhh@gmail.com)
- 💬 **Telegram**: [+8801616397082](https://t.me/+8801616397082)
- 📱 **WhatsApp**: [+8801616397082](https://wa.me/8801616397082)
- 🌐 **Portfolio**: [mahdi-hasan-shuvo.github.io](https://mahdi-hasan-shuvo.github.io/Mahdi-hasan-shuvo/)
- 💻 **GitHub**: [@Mahdi-hasan-shuvo](https://github.com/Mahdi-hasan-shuvo)

> *"Quality work speaks louder than words. Let's build something remarkable together."*


---

<p align="center">
  <sub>Built with ❤️ for seamless file synchronization</sub>
</p>
