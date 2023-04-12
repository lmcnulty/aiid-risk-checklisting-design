
The schema of the checklisting feature, in pseudocode:

```graphql
checklist {
  owner_user_id: UserID
  system_name: str
  description: MarkdownString
  query_classifications: [
    {
      namespace: str
      attribute_short_name: str

      # Not the same as the attribute's value_json.
      # value_json will be something like '["accident", "malice"]',
      # whereas the value here would be just be "malice".
      value: str       
    }
  ]
  risks: [
    {
      title: str
      status: 'Not Mitigated' | 'Mitigated' | 
              'Prevented'     | 'Not relevant'
      severity: str
      notes: MarkdownString
      precedents: [IncidentID]
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
