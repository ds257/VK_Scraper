
```markdown
# VK Data Scraper for Moldovan Election Content

This project is a Python-based scraper that uses the VK API to collect social media posts related to the 2024 Moldovan presidential election. By searching for relevant keywords (e.g., "Maia Sandu"), the script gathers posts, comments, engagement metrics, and media content from VK (VKontakte), a major social media platform in Eastern Europe. This data provides valuable insights into public sentiment, engagement, and discussions surrounding the election.

## Features

- **Multiple Account Rotation**: Uses multiple VK accounts for data collection, automatically rotating between them to avoid rate limits.
- **Targeted Keyword Search**: Collects posts based on specified keywords to ensure only relevant election-related data is gathered.
- **Engagement and Media Extraction**: Retrieves metrics like likes and comments, along with photos and videos attached to posts.
- **Iterative Data Collection**: Runs over multiple iterations, accumulating data in a JSON file for easy access and analysis.

## Getting Started

### Prerequisites

- **Python 3.x**: Ensure you have Python 3 installed.
- **VK API Library**: Install the `vk_api` Python library by running:
  ```bash
  pip install vk-api
  ```

### Installation

1. Clone or download this repository.
2. Install the required `vk_api` package if you haven’t done so.
3. Set up VK account credentials as described in the Configuration section.

### Configuration

Update the `accounts` list in the code with your VK account credentials:
```python
accounts = [
    {"user": "+14244027026", "pass": "JamieDOliver567"},
    {"user": "+14245223481", "pass": "RyanLAEmily123?."}
]
```

Each account is used sequentially to distribute API requests, minimizing the risk of hitting rate limits on any single account.

## Usage

Run the script to start collecting posts:
```bash
python vk_data_scraper.py
```

### Parameters

- **`max_iterations`**: Controls the number of times the script will iterate through account rotation and data collection. Adjust `max_iterations` in the `collect_posts` function to control the duration of the scraping session.

## API Utilization and Account Rotation

### Overview of VK API Usage

The VK API provides programmatic access to VK's public content, allowing this script to retrieve posts, comments, and engagement metrics efficiently. Key API endpoints used include:

- **`vk.newsfeed.search`**: Searches for posts matching specified keywords, targeting election-related content.
- **`vk.wall.getById`**: Retrieves detailed information about a post, such as its text content and engagement data (likes, comments).
- **`vk.wall.getComments`**: Collects comments on each post, enabling deeper insights into user opinions and discussions.
- **`vk.video.get`**: Fetches details about attached videos, adding context to posts with multimedia content.

### Account Rotation

To avoid VK’s API rate limits, this script supports account rotation:
1. **Multiple Accounts**: The script rotates through multiple VK accounts to maximize data collection while respecting rate limits.
2. **Automatic Account Switching**: Each iteration authenticates a new account, giving previously used accounts time to reset their rate limits.
3. **Retry Mechanism**: If an account fails to authenticate, the script waits briefly before retrying with the next account.

**Account Setup**:
Set up the `accounts` list with the necessary VK credentials:
```python
accounts = [
    {"user": "+14244027026", "pass": "JamieDOliver567"},
    {"user": "+14245223481", "pass": "RyanLAEmily123?."}
]
```

## Data Management

### Processed Posts Tracking

To avoid duplicate data, the script maintains a `processed_posts.json` file to track post IDs already collected. This file is updated after each iteration, preventing previously collected posts from being reprocessed.

### Data Storage and Structure

Collected data is stored in a JSON file (`vk_posts.json`). After each iteration, this file is updated, allowing real-time access to the cumulative dataset. Each post is stored with the following structure:
- **URL**: Link to the VK post.
- **Text**: Text content of the post.
- **Likes and Comments Counts**: Engagement data.
- **Comments**: List of comments on the post (if accessible).
- **Media**: Links to any photos or videos attached to the post.

### Example Data Structure

```json
{
  "url": "https://vk.com/wall543658724_61494",
  "text": "Election-related content...",
  "likes_count": 100,
  "comments_count": 20,
  "comments": [
    "This is an example comment",
    "Another comment"
  ],
  "photos": ["https://url_to_photo"],
  "videos": ["https://url_to_video"]
}
```

## Alternatives to VK API

If VK API limitations or platform access become a challenge, consider using other social media APIs for election-related data, such as:

- **Twitter API**: Ideal for tracking real-time discussions around election keywords and hashtags.
- **YouTube Data API**: Useful for gathering videos and comments on election-related videos.
- **News APIs** (e.g., News API): For gathering news articles from multiple sources, which can supplement social media data with journalistic perspectives.

## Stopping the Script

The script stops automatically after reaching the `max_iterations` limit. You can also stop it manually by pressing `Ctrl + C` during execution.

## Important Notes

- **Rate Limiting**: The VK API has rate limits; account rotation helps mitigate this.
- **Data Privacy**: Use the script responsibly and in compliance with VK’s terms of service.
- **Ethics**: Ensure that you use the collected data ethically and responsibly, particularly when handling user-generated content.


