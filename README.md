name: Weekly Marketing Trends Bot

on:
  schedule:
    # كل يوم اثنين الساعة 9 صباحاً بتوقيت مصر تقريباً (UTC+2/3)
    # وقت GitHub بيتوقيت UTC، فـ 9 صباحاً مصر = 7 صباحاً UTC تقريباً
    - cron: '0 7 * * 1'
  workflow_dispatch: {}
    # ده بيخليك تقدر تشغل البوت يدوياً من GitHub في أي وقت للتجربة

jobs:
  run-bot:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run the bot
        env:
          BOT_TOKEN: ${{ secrets.BOT_TOKEN }}
          CHAT_ID: ${{ secrets.CHAT_ID }}
        run: python marketing_trends_bot.py
