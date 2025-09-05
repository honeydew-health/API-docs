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
     "employment_terms": "Standard",
     "calendar_name": "Mon-Fri 8hr",
     "needs_engage_login": "true",
     "send_account_activation_email": "false",
     "custom_fields": {
        "pay_group": "PG001",
        "sick_pay_policy": "SSP",
        "country": "Scotland",
        "secondary_employee_id": "38475"
     }
  }' 
```

### JSON Parameters

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
department_name | string | <span class="label label-info">required*</span> Must match an existing department name. Must provide one of department_id, department_name or department_external_id.
department_id | integer | <span class="label label-info">required*</span> Must match an existing department id. Must provide one of department_id, department_name or department_external_id.
department_external_id | string | <span class="label label-info">required*</span> Must match an existing department external_id. Must provide one of department_id, department_name or department_external_id.
start_date | date | <span class="label label-info">required</span> Must be YYYY-MM-DD format. Employees start date in current role (not overall employment).
end_date | date | Must be YYYY-MM-DD format. Employees end date in current role.
first_manager_id | integer | Must match an existing employee id.
second_manager_id | integer | Must match an existing employee id.
employment_terms | string | Must match existing employment terms.
fte | decimal | Full-Time Equivalent for the employee's current role. Valid range: 0.01 to 2.00.
calendar_name | string | Must match existing calendar name.
needs_engage_login | boolean | Creates an Engage login for the employee, email required.
send_account_activation_email | boolean | <span class="label label-info">required*</span> Required if needs_engage_login provided.
custom_fields | string | Key/value pairs of existing custom fields. Key must be snake case.

<aside class="notice notice-info">
  Provide one of <code>department_name</code>, <code>department_id</code> or <code>department_external_id</code> to set department.
</aside>

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
     "first_manager_id": "456",
     "employment_terms": "Standard",
     "calendar_name": "Mon-Fri 8hr",
     "custom_fields": {
        "pay_group": "PG001",
        "sick_pay_policy": "SSP",
        "country": "Scotland",
        "secondary_employee_id": "38475"
     }
  }' 
```

### JSON Parameters

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
department_name | string | <span class="label label-info">required*</span> Must match an existing department name. Must provide one of department_id, department_name or department_external_id.
department_id | integer | <span class="label label-info">required*</span> Must match an existing department id. Must provide one of department_id, department_name or department_external_id.
department_external_id | string | <span class="label label-info">required*</span> Must match an existing department external_id. Must provide one of department_id, department_name or department_external_id.
start_date | date | <span class="label label-info">required*</span> Must be YYYY-MM-DD format. Employees start date in current role (not overall employment). Required unless end_date is provided and updating employee to leaver.
end_date | date | Must be YYYY-MM-DD format. Employees end date in current role. Ignored if new start date is provided.
first_manager_id | integer | Must match an existing employee id.
second_manager_id | integer | Must match an existing employee id.
employment_terms | string | Must match existing employment terms.
fte | decimal | Full-Time Equivalent for the employee's current role. Valid range: 0.01 to 2.00.
calendar_name | string | Must match existing calendar name.
needs_engage_login | boolean | Creates an Engage login for the employee, email required.
send_account_activation_email | boolean | <span class="label label-info">required*</span> Required if needs_engage_login provided.
custom_fields | string | Key/value pairs of existing custom fields. Key must be snake case.

<aside class="notice notice-info">
  Provide one of <code>department_name</code>, <code>department_id</code> or <code>department_external_id</code> to set department.
</aside>

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

<aside class="notice notice-info">
  <code>start_date</code> is not required to update an existing employee as a leaver. The provided <code>end_date</code> will be used to end the employees existing role.
</aside>

## Transfers

### Recommended additional minimum values for transfers

- start_date
- department_name
- first_manager_id
- second_manager_id

<aside class="notice notice-info">
  If a new <code>start_date</code> is given but <code>department_name</code> remains the same, the new <code>start_date</code> will be ignored and a transfer will not be recorded.
</aside>

<aside class="notice notice-info">
  Employees existing role will be ended 1 day before new <code>start_date</code>.
</aside>

<aside class="warning">
  Do not include an <code>end_date</code> for transferring active employees. Providing an <code>end_date</code> will process the employee as a leaver instead.
</aside>
