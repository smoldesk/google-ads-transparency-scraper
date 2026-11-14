# Google Ads Transparency Scraper

![Google Ads Transparency Scraper](https://raw.githubusercontent.com/smoldesk/apify-scrapers/main/assets/google-ads/banner.webp)

See every ad a competitor runs on Google Search, YouTube, Shopping, Maps and Play. Ad copy, images, landing pages, countries and dates. No login. Runs on [Apify](https://apify.com/smoldesk/google-ads-transparency-scraper).

## What you get

- **Ads by domain or advertiser**: type `nike.com` or a brand name, or paste an Ads Transparency Center URL.
- **Ad copy**: headline, description, call to action, business name, display URL and landing page.
- **Creatives**: image URLs, YouTube video ID and URL, and Shopping product title and merchant.
- **Reach**: first and last shown date, days shown, and every country the ad ran in.
- **Impressions and audience** for ads shown in the EU and for political ads.
- **Filters**: country, format (text, image, video), one or more platforms, date range, political ads only.
- **New ads only** mode for weekly competitor monitoring.
- **Advertisers mode**: who advertises for a brand or domain, one row per advertiser account with legal name, country, verified badge and ad count.
- **Account and campaign IDs** (`googleCustomerId`, `adGroupId`) and the advertiser's ad count on every ad.

## Run it

Open the [Google Ads Transparency Scraper on Apify](https://apify.com/smoldesk/google-ads-transparency-scraper), fill in the form and click Start. Or call it from code with your [Apify token](https://console.apify.com/settings/integrations):

```bash
curl -X POST "https://api.apify.com/v2/acts/smoldesk~google-ads-transparency-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "domains": ["booking.com", "expedia.com"],
    "regions": ["US", "DE"],
    "adFormat": "VIDEO",
    "platform": "YOUTUBE",
    "maxAdsPerSearch": 200,
    "includeDetails": true
  }'
```

## Sample output

```json
{
  "type": "ad",
  "advertiserName": "Booking.com",
  "creativeId": "CR07181948002024554497",
  "format": "text",
  "firstShown": "2022-02-22T08:00:00Z",
  "lastShown": "2026-10-18T13:29:08Z",
  "daysShown": 1208,
  "domain": "booking.com",
  "imageUrl": "https://tpc.googlesyndication.com/archive/simgad/14169895713917169526",
  "topic": "Travel & Tourism",
  "adType": "Commercial",
  "regionCount": 22,
  "regions": [
    {
      "country": "HU",
      "countryName": "Hungary",
      "firstShown": "2023-04-09",
      "lastShown": "2026-10-18",
      "impressionsMin": 0,
      "impressionsMax": 1000
    }
  ]
}
```

Export as JSON, CSV or Excel, or pipe it into Google Sheets, Make, Zapier or n8n.

## Pricing

Pay per result. No monthly fee. Prices drop on paid Apify plans.

| Result (per 1,000) | Free | Starter | Scale | Business |
|---|---|---|---|---|
| Ad with copy, image, landing page and dates | $1.00 | $1.00 | $0.90 | $0.75 |
| Full details add-on (countries, impressions, audience, variations) | +$2.00 | +$2.00 | +$1.75 | +$1.50 |
| Advertiser (Advertisers mode) | $2.00 | $2.00 | $1.75 | $1.50 |

Ads skipped by your filters or already seen in monitor mode are not charged.

## Limits

- Ad copy depends on what Google stores. In our test of 500 US ads, text fields were filled for about 80% of video ads and 40% of image ads.
- Search text ads are mostly stored as a screenshot. You get it in `imageUrl`, but `headline` stays empty.
- Impressions and audience exist only for EU and political ads. Other countries get first and last shown dates.
- The Center lists verified advertisers back to about 2020.
- Account and campaign IDs come from Google's preview script, so ads stored only as an image have none.

## FAQ

**Is there a Google Ads Transparency Center API?**
No public one. This reads the same data the Center shows in the browser and returns it as JSON.

**How do I find all ads of a competitor?**
Put their domain in `domains`. Use `advertisers` for a name, and `advertisersPerName` (0 = all) if several advertisers share it. Set `resultType` to `advertisers` to list the accounts first.

**How do I get alerts for new ads?**
Turn on `onlyNewAds` and schedule the run weekly. Only creatives not seen in earlier runs are returned and charged.

**Can I get the ad images and videos?**
Yes. `imageUrls` holds the images and `youtubeUrl` the video for video ads.

**Does it cover the Meta (Facebook) Ad Library?**
No. Google ads only.

## More scrapers

Google Ads Transparency is one of 21 no-login scrapers by Smoldesk Studios. See the full list: [smoldesk/apify-scrapers](https://github.com/smoldesk/apify-scrapers).
