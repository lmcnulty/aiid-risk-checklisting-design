Risks are surfaced based on classification tags applied
by taxonomy editors of the AI Incident Database.
To find tags available to search by:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/search_tags"
  -X POST -H "Content-Type: application/json" --data '{ "limit": 20 }'
```
```json
{
  "search_tags": [
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

To find risks matching a set of tags,
ordered by the number of matches:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risks" \
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
          "url": "https://incidentdatabase.ai/cite/146",
          "title": "Research Prototype AI, Delphi, Reportedly Gave Racially Biased Answers on Ethics",
          "description": "A publicly accessible research model[...]moral judgments.",
          "search_tags": [
            "GMF:Known AI Technology:Language Modeling",
            "GMF:Known AI Goal:Question Answering",
            "GMF:Known AI Technology:Distributional Learning"
          ],
          "risk_tags": [
            "GMF:Known AI Technical Failure:Distributional Bias",
            "GMF:Failure:Gaming Vulnerability"
          ]
        },
        {
          "incident_id": 72,
          "url": "https://incidentdatabase.ai/cite/72",
          "title": "Facebook translates 'good morning' into 'attack them'",
          "description": "Facebook's automatic language[...]in Beitar Illit, Israel.",
          "search_Tags": [
            "GMF:Known AI Technology:Language Modeling"
          ],
          "risk_tags": [
            "GMF:Failure:Gaming Vulnerability"
          ]
        }
      ]
    }
  ]
}
```

A JSON objects containing the full 

If no tags are in the query, every risk up to `limit` is returned.

Suppose it's been some time and you want to find 
risks surfaced since the last search.
You can provide a date cutoff:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risks" \
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
          "url": "https://incidentdatabase.ai/cite/470",
          "title": "Bing Chat Response Cited ChatGPT Disinformation Example",
          "description": "Reporters from TechCrunch[...]substantiate the disinformation.",
          "search_tags": [
            "GMF:Known AI Technology:Language Modeling",
            "GMF:Known AI Goal:Question Answering"
          ],
          "risk_tags": [
            "GMF:Known AI Technical Failure:Misinformation Generation Hazard"
          ]
        }
      ]
    }
  ]
}
```

The above only surfaces new risks. 
If you want to get new *precedent incidents* 
for new *and* existing risks,
you can do so with:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risks" \
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
          "url": "https://incidentdatabase.ai/cite/470",
          "title": "Bing Chat Response Cited ChatGPT Disinformation Example",
          "description": "Reporters from TechCrunch[...]substantiate the disinformation.",
          "search_tags": [
            "GMF:Known AI Technology:Language Modeling",
            "GMF:Known AI Goal:Question Answering"
          ],
          "risk_tags": [
             "GMF:Known AI Technical Failure:Misinformation Generation Hazard"
          ]
        }
      ]
    },
    {
      "tag": "GMF:Failure:Gaming Vulnerability",
      "precedents": [
        {
          "incident_id": 420,
          "url": "https://incidentdatabase.ai/cite/420",
          "title": "Users Bypassed ChatGPT's Content Filters with Ease",
          "description": "Users reported bypassing[...]or generate harmful content.",
          "search_tags": [
            "GMF:Known AI Technology:Language Modeling"
          ],
          "risk_tags": [
            "GMF:Failure:Gaming Vulnerability"
          ]
        }
      ]
    }
  ]
}
```

You can access a precedent by ID:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/precedent"
  -X POST -H "Content-Type: application/json" --data '{ "incident_id": 146 }'
```
```json
{
  "incident_id": 146,
  "url": "https://incidentdatabase.ai/cite/146",
  "title": "Research Prototype AI, Delphi, Reportedly Gave Racially Biased Answers on Ethics",
  "description": "A publicly accessible research model[...]moral judgments.",
  "search_tags": [
    "GMF:Known AI Technology:Language Modeling",
    "GMF:Known AI Goal:Question Answering",
    "GMF:Known AI Technology:Distributional Learning"
  ],
  "risk_tags": [
    "GMF:Known AI Technical Failure:Distributional Bias",
    "GMF:Failure:Gaming Vulnerability"
  ]
}
```

You can get all known risk tags in the same manner as search tags:

```bash
$ curl "https://incidentdatabase.ai/api/riskManagement/v1/risk_tags"
  -X POST -H "Content-Type: application/json" --data '{ "limit": 20 }'
```
```json
{
  "risk_tags": [
    "GMF:Known AI Technical Failure:Unsafe Exposure or Access",
    "GMF:Known AI Technical Failure:Distributional Bias",
    "GMF:Known AI Technical Failure:Misuse",
    "GMF:Known AI Technical Failure:Adversarial Data",
    "GMF:Known AI Technical Failure:Limited Dataset",
    "GMF:Known AI Technical Failure:Black Swan Event",
    "GMF:Known AI Technical Failure:Data or Labelling Noise",
    "GMF:Known AI Technical Failure:Dataset Imbalance",
    "GMF:Known AI Technical Failure:Generalization Failure",
    "GMF:Known AI Technical Failure:Lack of Adversarial Robustness",
    "GMF:Known AI Technical Failure:Underfitting",
    "GMF:Known AI Technical Failure:Tuning Issues",
    "GMF:Known AI Technical Failure:Inappropriate Training Content",
    "GMF:Known AI Technical Failure:Inadequate Anonymization",
    "GMF:Known AI Technical Failure:Unauthorized Data",
    "GMF:Known AI Technical Failure:Underspecification",
    "GMF:Known AI Technical Failure:Context Misidentification",
    "GMF:Known AI Technical Failure:Gaming Vulnerability",
    "GMF:Known AI Technical Failure:Lack of Capability Control",
    "GMF:Known AI Technical Failure:Concept Drift",
    "GMF:Known AI Technical Failure:Misinformation Generation Hazard"
  ]
}
```

Incident data not included in the risk management API
can be accessed via our GraphQL API at
<https://incidentdatabase.ai/api/graphql>.
documented at in our [README](https://github.com/responsible-ai-collaborative/aiid#public-graphql-endpoint).
Example:

```graphql
query {
  incidents(query: { incident_id:470 }) {
    date
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
