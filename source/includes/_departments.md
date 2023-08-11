# Departments

## List departments
`GET /api/v1/departments`

```
curl -X GET /api/v1/departments \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json"
```

> Example JSON Response:

```
[
  {
    "id": "1",
    "external_id": "abc1",
    "name": "abc",
    "parent_department_id": null,
    "parent_department_external_id": null,
    "parent_department": null,
    "created_at": "2022-09-01T14:15:59.000+01:00",
    "updated_at": "2022-09-01T14:15:59.000+01:00",
    "retired_at": null
  },
  {
    "id": "2",
    "external_id": "xyz2",
    "name": "xyz",
    "parent_department_id": "1",
    "parent_department_external_id": "abc1",
    “parent_department": "abc",
    "created_at": "2022-09-01T14:15:59.000+01:00",
    "updated_at": "2022-09-01T14:15:59.000+01:00",
    "retired_at": null
  }
]
```

### Query Parameters

Name | Type | Description
--------- | ------- | -----------
parent_department_id | integer | Id of parent department to filter by.
parent_department_external_id | string | Your id of parent department to filter by.

## Get a department
`GET /api/v1/departments/{id}`

`GET /api/v1/departments/external_id/{id}`

> Using our Id:

```
curl -X GET /api/v1/departments/123 \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json"
```

> Using your Id:

```
curl -X GET /api/v1/departments/external_id/abc123 \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json"
```

> Example JSON Response:

```
{
  "id": "123",
  "external_id": "abc123",
  "name": "abc",
  "parent_department_id": null,
  "parent_department_external_id": null,
  "parent_department": null,
  "created_at": "2022-09-01T14:15:59.000+01:00",
  "updated_at": "2023-08-01T14:15:59.000+01:00",
  "retired_at": null
}
```

## Update a department
`PUT /api/v1/departments/{id}`

`PUT /api/v1/departments/external_id/{external_id}`

> Using our id:

```
curl -X PUT /api/v1/departments/123 \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "name": "abc"
  }' 
```

> Using your id:

```
curl -X PUT /api/v1/departments/external_id/abc123 \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "name": "abc"
  }' 
```

> Example JSON Response:

```
{
  "id": "123",
  "external_id": "abc123",
  "name": "abc",
  "parent_department_id": null,
  "parent_department_external_id": null,
  "parent_department": null,
  "created_at": "2022-09-01T14:15:59.000+01:00",
  "updated_at": "2023-08-01T14:15:59.000+01:00",
  "retired_at": null
}
```

### JSON Parameters

Name | Type | Description
--------- | ------- | -----------
name | string | <span class="label label-info">required</span> Unique department name.
external_id | string | Your unique identifier for the department, 25 character max.
parent_department | string | Name of the existing parent department.
parent_department_id | string | Id of the existing parent department.
parent_department_external_id | string | Your unique identifier for the existing parent department.

<aside class="notice notice-info">
  Provide one of <code>parent_department</code>, <code>parent_department_id</code> or <code>parent_department_external_id</code> to set parent department.
</aside>

## Retire a department
`PUT /api/v1/departments/{id}/retire`

`PUT /api/v1/departments/external_id/{external_id}/retire`

> Using our id:

```
curl -X PUT /api/v1/departments/123/retire \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "retire_at": "2023-08-01",
     "employee_action": "retire"
  }' 
```

> Using your id:

```
curl -X PUT /api/v1/departments/external_id/abc123/retire \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "retire_at": "2023-08-01",
     "employee_action": "transfer",
     "transfer_department_external_id": "abc123"
  }' 
```

> Example JSON Response:

```
{
  "id": "123",
  "external_id": "abc123",
  "name": "abc",
  "parent_department_id": null,
  "parent_department_external_id": null,
  "parent_department": null,
  "created_at": "2022-09-01T14:15:59.000+01:00",
  "updated_at": "2023-08-01T14:15:59.000+01:00",
  "retired_at": "2023-08-01T00:00:00.000+01:00"
}
```

### JSON Parameters

Name | Type | Description
--------- | ------- | -----------
retire_at | date | <span class="label label-info">required</span> Must be YYYY-MM-DD format.
employee_action | string | `retire` or `transfer`. Defaults to `retire`.
sub_department_action | string | `retire` or `promote`. Defaults to `retire`.
transfer_department_id | integer | <span class="label label-info">required*</span> Required if employee action = `transfer` and `transfer_department_external_id` not provided.
transfer_department_external_id | string | <span class="label label-info">required*</span> Required if employee action = `transfer` and `transfer_department_id` not provided.

### Employee Action

Name | Description
----- | ----------
retire | Employees current role will be ended.
transfer | Employees current role will be ended and a new role started at transfer department.

### Sub Department Action

Name | Description
----- | ----------
retire | Sub departments will be retired.
promote | Sub departments will be promoted to level of retiring department.
