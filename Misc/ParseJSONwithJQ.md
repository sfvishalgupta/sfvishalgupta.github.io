#### [Back](./README.md)

# Parse JSON data with JQ

[Tutorial](https://www.digitalocean.com/community/tutorials/how-to-transform-json-data-with-jq)


Parse Unix timestamp to get Year.
```angular2html
jq '.event_timestamp | strftime("%Y")' seaCreatures.json
```