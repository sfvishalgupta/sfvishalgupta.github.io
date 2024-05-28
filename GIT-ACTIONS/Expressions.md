#### [Back](./README.md)

# Expressions

Example of setting Env Variable
```yaml
env:
  MY_ENV_VAR: ${{ <expression> }}
```

## Literals
```yaml
env:
  myNull: ${{ null }}
  myBoolean: ${{ false }}
  myIntegerNumber: ${{ 711 }}
  myFloatNumber: ${{ -9.2 }}
  myHexNumber: ${{ 0xff }}
  myExponentialNumber: ${{ -2.99e-2 }}
  myString: Mona the Octocat
  myStringInBraces: ${{ 'It''s open source!' }}
```

## Operators
```yaml
env:
  MY_ENV_VAR: ${{ github.ref == 'refs/heads/main' && 'value_for_main_branch' || 'value_for_other_branches' }}
```

## Functions

### contains
**contains( search, item )**

```yaml
// String Filter
contains('Hello world', 'llo') // return true

// Object Filter
contains(github.event.issue.labels.*.name, 'bug')

// check form array
contains(fromJSON('["push", "pull_request"]'), github.event_name)
```

### startsWith
### endsWith
### format
### join
### toJSON
### fromJSON
### hashFiles
### Status check function
```yaml
steps:
  ...
  - name: The job has succeeded
    if: ${{ success() }}
```
### always
### cancelled
### failure
### failure with conditions


## Object Filter
You can use the * syntax to apply a filter and select matching items in a collection.

```json
[
  { "name": "apple", "quantity": 1 },
  { "name": "orange", "quantity": 2 },
  { "name": "pear", "quantity": 1 }
]
```
The filter **fruits.*.name** returns the array **[ "apple", "orange", "pear" ]**.