# Bluesky Post Labeling Bot

A Bluesky bot that rates how "safe" posts are with a large language model. Mention
`@sentiment_bot` in a post, and the bot reads the author's two latest posts, asks an LLM for a
safety score from 0 to 100, and replies with the score. Posts about politics, violence, shocking
news and similar topics score below 50.

The notebook also scores a sample of historical posts in bulk and saves the results to Excel.

## How it works

- Listens to the Bluesky firehose (the live stream of all posts) with
  [atproto](https://atproto.blue).
- Sends post text to Mixtral 8x7B (live bot) or Llama 2 7B (bulk scoring) through
  [Replicate](https://replicate.com).
- Replies to the post through the Bluesky API.

## Getting started

1. Install Python 3.10 or newer, then:

   ```bash
   pip install -r requirements.txt
   ```

2. Copy `.env.example` to `.env` and fill in your Replicate API token and your Bluesky handle and
   app password. Use an [app password](https://bsky.app/settings/app-passwords), not your main
   password. `.env` is in `.gitignore` and never gets committed.

3. Open `BskySocial_Labeling_Bot/Bsky_PostLabeling.ipynb` and run the first two cells to start
   the bot. It runs until you stop the kernel.

The bulk-scoring cells read `sampled_posts.csv` (a CSV with a `text` column), which is not
included in this repo. Each Replicate call costs a small amount of money.

## License

Licensed under the [Apache License 2.0](LICENSE).
