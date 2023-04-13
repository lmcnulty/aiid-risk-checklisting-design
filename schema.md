
The schema of the checklisting feature, in pseudocode:

```graphql
checklist {
  owner_user_id: UserID
  system_name: str  # Fairly lists by project -- could change in the UI
  description: MarkdownString # "About System" in the UI

  #
  # For example, you might generate a list of technical failure risks
  # with a query for `GMF:Known AI Technology:Transformers`.
  # grouped by `GMF:Known AI Technical Failure`.
  #
  # You might *additionally* generate a list of bias risks 
  # with a query for `GMF:Known AI Goal:Question answering`
  # grouped by `CSET:Harm Distribution Basis`.
  #
  # The generated risks would both be added to the `checklist.risks`,
  # including as new matching classifications
  # are added to the database.
  #
  risk_queries: [
    { 
      attributes: [
        {
          namespace: str             # e.g. "GMF"
          attribute_short_name: str  # e.g. "Known AI Technology"

          # Not the same as the attribute's value_json.
          # value_json will be e.g. '["Transformers", "Regression"]',
          # whereas the value here would be just be "Transformers".
          value: str       
        }
      ]
      group_by_attribute: {
        namespace: str   # e.g. "GMF"
        short_name: str  # e.g. "Known AI Technical Failure"
                         #       ^^^^^
                         # We might also want to special-case 
                         # GMF taxonomy queries to include
                         # known *and* potential xyz.
      }
    }
  ]
  risks: [
    {
      # When a risk is added by a risk query,
      # the title will be set to based on
      # the group_by_classification value.
      # So if grouping by `CSET:Harm Distribution Basis`
      # the title could be set to `CSET:Harm Distribution Basis:Race`.
      title: str

      severity: str              # Severity labels are user-defined
      notes: MarkdownString
      precedents: [IncidentID]
      status: 'Not Mitigated' | 'Mitigated' | 
              'Prevented'     | 'Not relevant'
      # 
      # When a new risk is added by a risk query,
      # this will be copied from risk_queries[i].classifications
      # where risk_queries[i] is the query that generated the risk.
      #
      # If the risk is added manually,
      # this starts out empty but can be added.
      #
      precedents_query_attributes: [
        {
          namespace: str
          attribute_short_name: str
          value: str       
        }
      ]

      new_precedent_subscribers: [UserID]

      # The API is based on polling based on
      # the date of the consumer's last update.
      # However, for email notifications, etc.
      # generated from within our system,
      # we need to track the last time we pushed
      # new results to the subscribers.
      last_subscription_push: DateTime
    }
  ]
  new_risk_subscribers: [UserID]
  last_subscription_push: DateTime
}
```

We will need to extend the classifications schema
to include the modification date

```graphql
classification {
  ...
  attributes: [
    { 
      ...
      last_modified: DateTime
    }
  ]
}
```

In the mockup, users have names that can be displayed:

```graphql
  user {
    ...
    name: str
  }
```

We might also want to label certain taxonomy attributes
as default options for risk querying and grouping.

```graphql
  taxa {
    field_list: [
      {
        ...
        default_risk_query: bool
        default_risk_group: bool
      }
    ]
  }
```



