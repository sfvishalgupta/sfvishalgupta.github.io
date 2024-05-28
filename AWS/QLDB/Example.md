#### [Back](./README.md)

# Examples of AWS QLDB

The table hr.employees is denoted in the PartiQL data model as this dataset

```json
{
  'hr': {
    'employees': <<
      -- a tuple is denoted by { ... } in the PartiQL data model
      { 'id': 3, 'name': 'Bob Smith',   'title': null },
      { 'id': 4, 'name': 'Susan Smith', 'title': 'Dev Mgr' },
      { 'id': 6, 'name': 'Jane Smith',  'title': 'Software Eng 2'}
    >>
  }
}
```

* **employees** is nested within **hr**
* The delimiters **<< …​ >>** denote that the data is an **unordered** collection (also known as **bag**),
* That is, there is no order between the three **tuples**. 
* Single-line comments start with -- and end at the end of the line.

Set of json files which contains following json object

```json
{
  "hr" : {
    "employees": [
      { "id": 3, "name": "Bob Smith",   "title": null },
      { "id": 4, "name": "Susan Smith", "title": "Dev Mgr" },
      { "id": 6, "name": "Jane Smith",  "title": "Software Eng 2"}
    ]
  }
}
```

**Query to get Data**

```text
SELECT e.id, e.name AS employeeName, e.title AS title FROM hr.employees e 
WHERE e.title = 'Dev Mgr'
```

**Output**
```json
<<
  {
    'id': 4,
    'employeeName': 'Susan Smith',
    'title': 'Dev Mgr'
  }
>>
```

**The result remains the same, no matter whether hr.employees is a SQL table or a JSON file.**

### Nested Collection

```json
{
  'hr': {
    'employeesNest': <<
      {
        'id': 3,
        'name': 'Bob Smith',
        'title': null,
        'projects': [
          { 'name': 'AWS Redshift Spectrum querying' },
          { 'name': 'AWS Redshift security' },
          { 'name': 'AWS Aurora security' }
        ]
      },
      {
        'id': 4,
        'name': 'Susan Smith',
        'title': 'Dev Mgr',
        'projects': []
      },
      {
        'id': 6,
        'name': 'Jane Smith',
        'title': 'Software Eng 2',
        'projects': [ { 'name': 'AWS Redshift security' } ]
      }
    >>
  }
}
```

**Query**
```text
SELECT e.name AS employeeName, p.name AS projectName
FROM hr.employeesNest AS e, e.projects AS p
WHERE p.name LIKE '%security%'
```

**Result**
```json
<<
  {
    'employeeName': 'Bob Smith',
    'projectName': 'AWS Redshift security'
  },
  {
    'employeeName': 'Bob Smith',
    'projectName': 'AWS Aurora security'
  },
  {
    'employeeName': 'Jane Smith',
    'projectName': 'AWS Redshift security'
  }
>>
```
