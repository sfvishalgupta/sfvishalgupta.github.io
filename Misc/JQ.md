#### [Back](./README.md)

# Bash JQ

**jq** is a lightweight, command-line JSON processor.

* ### Array Indexing
```bash
echo "[1,2,3,4,5]" | jq '.[2:4]' ### [3,4]
echo "[1,2,3,4,5]" | jq '.[2:]'  ### [3,4,5]
echo "[1,2,3,4,5]" | jq '.[-2:]' ### [4,5]
```

* ### JQ Options
    * **-r**    Removing double quotes (give raw String instead)
    * **-j**    option (for join) can combine together your output.
    * **-S**    Sort keys
    * **-R**    Raw Input
    * **-c**    compact output