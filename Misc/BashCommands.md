#### [Back](./README.md)

* ### Read Json file property via JC from File
```shell
jq .Description test.json
```

* ### Read Json file property via JC from String
```shell
str={Description:""}
jq .Description <<< "$str"
```

* ### Read Json file via JC with Filters
```shell
jq -c '.items[] | select(.path=="/") | .resourceMethods' test.json
```

* ### Remove Double quotes from String
```shell
tr -d '"'
```

* ### Split a String and Access by Index
```shell
arn="aws:ddb.........."
arrIN=(${arn//$AWS_ACCOUNT_ID:/ })
api_id=${arrIN[1]}
```

* ### Get DDB Table Name from ARN
```shell
function getDDBTableNameFromArn() {
    arn=$1
    arrIN=(${arn//:table\// })
    tmpstr=${arrIN[1]}
    tmparr1=(${tmpstr//\// })
    tableName=${tmparr1[0]}
    echo $tableName
}
```

* ### Replace String
```shell
tmp="${tfvars_template/ENV/dev}"
```

* ### Grep output into variable with number of lines
```shell
str=$(grep -Rl "POST" test.json | wc -l | xargs)
if [ "$str" -gt 0 ]; then
    echo "Found $str times"
fi
```

* ### Remove String via tr
```shell
echo "hi" | tr -d "\n"
```

* ### Replace String via tr
```shell
echo "hi" | tr " " ","
```

* ### Replace String via sed
```shell
echo "$keys" | sed -r 's/[xyz]+/_/g'
```


