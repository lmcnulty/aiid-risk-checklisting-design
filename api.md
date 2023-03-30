Risks are surfaced based on classification tags applied
by taxonomy editors of the AI Incident Database.
To find tags available to search by:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/search_tags"
  -X POST -H "Content-Type: application/json" --data '{ "limit": 20 }'
```
```json
{
  "searchTags": [
    "GMF:Known AI Technology:Character NGrams",
    "GMF:Known AI Technology:Acoustic Triangulation",
    "GMF:Known AI Technology:Transformer",
    "GMF:Known AI Technology:Diverse Data",
    "GMF:Known AI Goal:Content Search",
    "GMF:Known AI Goal:Scheduling",
    "GMF:Known AI Goal:Content Recommendation",
    "GMF:Known AI Goal:Chatbot",
    "GMF:Known AI Technology:Gesture Recognition",
    "GMF:Known AI Goal:Audio Localization",
    "GMF:Known AI Technology:Optical Character Recognition",
    "GMF:Known AI Goal:Question Answering",
    "GMF:Known AI Technology:Regression",
    "GMF:Known AI Goal:Market Forecasting",
    "GMF:Known AI Goal:Automatic Skill Assessment",
    "GMF:Known AI Technology:Classification",
    "GMF:Known AI Goal:NSFW Content Detection",
    "GMF:Known AI Technology:Autoencoder",
    "GMF:Known AI Technology:Multimodal Learning",
    "GMF:Known AI Technology:Image Segmentation"
  ]
}
```

To find risks matching a set of tags:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risk_tags" \
  --request POST --header "Content-Type: application/json" \
  --data '{
    "tags": [
      "GMF:Known AI Technology:Language Modeling",
      "GMF:Known AI Goal:Question Answering"
    ]
  }'
```
```json
{
  "risks": [
    {
      "tag": "GMF:Failure:Gaming Vulnerability",
      "precedents": [
        {
          "incident_id": 146,
          "title": "Research Prototype AI, Delphi, Reportedly Gave Racially Biased Answers on Ethics",
          "matching_tags": [
            "GMF:Known AI Technology:Language Modeling",
            "GMF:Known AI Goal:Question Answering"
          ]
        },
        {
          "incident_id": 72,
          "title": "Facebook translates 'good morning' into 'attack them'",
          "matching_tags": [
            "GMF:Known AI Technology:Language Modeling"
          ]
        }
      ]
    }
  ]
}
```

Suppose it's been some time and you want to find 
risks surfaced since the last search.
You can provide a date cutoff:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risk_tags" \
  --request POST --header "Content-Type: application/json" \
  --data '{
    "tags": [
      "GMF:Known AI Technology:Language Modeling",
      "GMF:Known AI Goal:Question Answering"
    ],
    "risks_added_since": "2022-11-01"
  }'
```
```json
{
  "risks": [
    {
      "tag": "GMF:Known AI Technical Failure:Misinformation Generation Hazard",
      "precedents": [
        {
          "incident_id": 470,
          "title": "Bing Chat Response Cited ChatGPT Disinformation Example",
          "matching_tags": [
            "GMF:Known AI Technology:Language Modeling",
            "GMF:Known AI Goal:Question Answering"
          ]
        }
      ]
    },
    {
      "tag": "GMF:Failure:Gaming Vulnerability",
      "precedents": [
        {
          "incident_id": 420,
          "title": "Users Bypassed ChatGPT's Content Filters with Ease",
          "matching_tags": [
            "GMF:Known AI Technology:Language Modeling"
          ]
        }
      ]
    }
  ]
}
```

The above only surfaces new risks. 
If you want to get new *precedent incidents* for new *and* existing risks,
you can do so with:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risk_tags" \
  --request POST --header "Content-Type: application/json" \
  --data '{
    "tags": [
      "GMF:Known AI Technology:Language Modeling",
      "GMF:Known AI Goal:Question Answering"
    ],
    "precedents_added_since": "2022-11-01"
  }'
```
```json
{
  "risks": [
    {
      "tag": "GMF:Known AI Technical Failure:Misinformation Generation Hazard",
      "precedents": [
        {
          "incident_id": 470,
          "title": "Bing Chat Response Cited ChatGPT Disinformation Example",
          "matching_tags": [
            "GMF:Known AI Technology:Language Modeling",
            "GMF:Known AI Goal:Question Answering"
          ]
        }
      ]
    }
  ]
}
```


All data on a given incident can be obtained via our GraphQL API

```graphql
query {
  incidents(query: { incident_id:470 }) {
    date
    description
    reports {
      title
      url
    }
  }
}
```
```json
{
  "data": {
    "incidents": [
      {
        "date": "2023-02-08",
        "description": "Reporters from TechCrunch issued a query to Microsoft Bing's ChatGPT feature, which cited an earlier example of ChatGPT disinformation discussed in a news article to substantiate the disinformation.",
        "reports": [
          {
            "title": "AI is eating itself: Bing's AI quotes COVID disinfo sourced from ChatGPT",
            "url": "https://techcrunch.com/2023/02/08/ai-is-eating-itself-bings-ai-quotes-covid-disinfo-sourced-from-chatgpt/"
          }
        ]
      }
    ]
  }
}
```
