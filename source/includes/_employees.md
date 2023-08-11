# Employees

## Create an employee
`POST /api/v1/employees`

```
curl -X POST /api/v1/employees \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "employee_id": "123",
     "first_name": "Joe",
     "surname": "Bloggs",
     "date_of_birth": "1980-04-23",
     "email": "joe.bloggs@example.com",
     "job_title": "Administrative Assistant",
     "department_name": "HR",
     "start_date": "2023-08-01",
     "first_manager_id": "456",
     "needs_engage_login": "true",
     "send_account_activation_email": "false"
  }' 
```

### Parameters

Name | Type | Description
--------- | ------- | -----------
employee_id | string | <span class="label label-info">required</span> Your unique identifier for the employee.
first_name | string | <span class="label label-info">required</span>
middle_name | string | 
surname | string | <span class="label label-info">required</span>
date_of_birth | date | Must be YYYY-MM-DD format.
email | string | <span class="label label-info">required*</span> Required if needs_engage_login true.
mobile | string | 
job_title | string | Must match an existing job title. Reporting by job title must be enabled in company settings if provided. Invalid values ignored. 
department_name | string | <span class="label label-info">required</span> Must match an existing department name.
start_date | date | <span class="label label-info">required</span> Must be YYYY-MM-DD format. Employees start date in current role (not overall employment).
end_date | date | Must be YYYY-MM-DD format. Employees end date in current role.
first_manager_id | integer | Must match an existing employee id.
second_manager_id | integer | Must match an existing employee id.
needs_engage_login | boolean | Creates an Engage login for the employee, email required.
send_account_activation_email | boolean | <span class="label label-info">required*</span> Required if needs_engage_login provided.

## Update an employee
`PUT /api/v1/employees`

```
curl -X PUT /api/v1/employees \
  -H "Authorization: Bearer abc" \
  -H "Content-Type: application/json" \
  -d '{
     "employee_id": "123",
     "first_name": "Joe",
     "surname": "Bloggs",
     "date_of_birth": "1980-04-23",
     "email": "joe.bloggs@example.com",
     "job_title": "Administrative Assistant",
     "department_name": "HR",
     "start_date": "2023-08-01",
     "end_date": "2023-08-30",
     "first_manager_id": "456"
  }' 
```

### Parameters

Name | Type | Description
--------- | ------- | -----------
employee_id | string | <span class="label label-info">required</span> Your unique identifier for the employee.
first_name | string | <span class="label label-info">required</span>
middle_name | string | 
surname | string | <span class="label label-info">required</span>
date_of_birth | date | Must be YYYY-MM-DD format.
email | string | <span class="label label-info">required*</span> Required if needs_engage_login true.
mobile | string | 
job_title | string | Must match an existing job title. Reporting by job title must be enabled in company settings if provided. Invalid values ignored. 
department_name | string | <span class="label label-info">required</span> Must match an existing department name.
start_date | date | <span class="label label-info">required</span> Must be YYYY-MM-DD format. Employees start date in current role (not overall employment).
end_date | date | Must be YYYY-MM-DD format. Employees end date in current role. Ignored if new start date is provided.
first_manager_id | integer | Must match an existing employee id.
second_manager_id | integer | Must match an existing employee id.
needs_engage_login | boolean | Creates an Engage login for the employee, email required.
send_account_activation_email | boolean | <span class="label label-info">required*</span> Required if needs_engage_login provided.

## Employee logins

If you need for the employee to login to Engage, you can provide the `needs_engage_login` and `send_account_activation_email` fields to provision their user account. By default the employee will not be able to login.

### send_account_activation_email

For companies with SSO enabled, this will send a welcome email to the employee advising them that they can now login with their company email.

For companies without SSO enabled, this will send a welcome email to the employee with a secure link from which they can set their password and login.

## New starters

### Recommended additional minimum values for new starters

- first_manager_id
- second_manager_id

## New managers

### Recommended additional minimum values for new managers

- email
- mobile
- first_manager_id
- second_manager_id

## Leavers

### Recommended additional minimum values for leavers

- end_date

## Transfers

### Recommended additional minimum values for transfers

- start_date
- department_name
- first_manager_id
- second_manager_id
