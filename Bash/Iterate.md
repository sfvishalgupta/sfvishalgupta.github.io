#### [Back](./README.md)

# Iterate Over Folders
```bash

#!/bin/usr/env bash
myArray=(
    "./services"
)
for str in ${myArray[@]}; do
    echo "Scanning Directory $str"
    for dir in $str/*/          # list directories in the form "/tmp/dirname/"
    do
        dir=${dir%*/}           # remove the trailing "/"
        echo "${dir##*/}"       # print everything after the final "/"
    done
done
```