# Job Titles

## Create a job title
`POST /api/v1/job_titles`

```
curl -X POST /api/v1/job_titles \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "title": "abc"
  }' 
```

### Parameters

Name | Type | Description
--------- | ------- | -----------
title | string | <span class="label label-info">required</span> Unique job title.
