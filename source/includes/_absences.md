# Absences

## List absences
`GET /api/v1/absences`

```
curl -X GET /api/v1/absences?start_date=2019-04-18 \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json"
```

> Example JSON Response:

```
[
  {
    "absence_id": "372846",
    "employee_id": "11223344",
    "start_date": "2019-04-18",
    "confirmed_return_date": null,
    "end_date": null,
    "created_at": "2019-04-18 18:01:57", 
    "updated_at": "2019-04-18 18:01:57", 
    "absence_cause": "Flu",
    "absence_cause_category": "Infections",
    "half_day_start": 0,
    "half_day_end": 1,
  },
  {
    "absence_id": "372847",
    "employee_id": "11223344",
    "start_date": "2019-04-18",
    "confirmed_return_date": "2019-04-19",
    "end_date": "2019-04-18",
    "created_at": "2019-04-18 18:01:57",
    "updated_at": "2019-04-18 18:01:57", 
    "absence_cause": "Flu",
    "absence_cause_category": "Infections",
    "half_day_start": "0",
    "half_day_end": "0",
  }
]
```

### Query Parameters

Name | Type | Description
--------- | ------- | -----------
start_date | date | Must be YYYY-MM-DD format. Matches equal to or greater than.
confirmed_return_date | date | Must be YYYY-MM-DD format. Matches equal to or greater than.
created_at | date | Must be YYYY-MM-DD format. Matches equal to or greater than.
updated_at | date | Must be YYYY-MM-DD format. Matches equal to or greater than.

<aside class="warning">
  <strong>At least one</strong> query parameter required.
</aside>

<aside class="notice notice-info">
  <code>absence_cause</code> and <code>absence_cause_category</code> only returned if privacy settings allow. See Administration > Preferences > Data API on your Engage Account.
</aside>
