#### [Back](./README.md)

# Download the List of All IOT Devices via AWS CLI AS CSV File 

Below is the script for downloading the list of all IOT Devices from the AWS via AWS CLI.

1. You shoule have aws cli properly setup.
2. Node Should be installed.
3. Packages required for running the script are 
   child_process
   fs

4. Below script will download all things with Thing type name ABC1, assuming file name is **export.js**

```js
"use strict";
const { exec } = require("child_process");
const fs = require("fs");
const byDevice = "ABC1";
const arr = [["Thing Name", "Thing Type", "Arn", "Version"]];
const command = "aws iot list-things --max-items 200 ";
const exportThings = (NextToken) => {
    let command1 = command;
    if (byDevice.length > 0) {
        command1 += " --thing-type-name  " + byDevice + " ";
    }
    if (NextToken) {
        command1 += " --starting-token " + NextToken;
    }
    console.log("Executing command :- " + command1);
    exec(command1, (error, stdout, stderr) => {
        if (error) {
            console.log(`error: ${error.message}`);
            return;
        }
        if (stderr) {
            console.log(`stderr: ${stderr}`);
            return;
        }
        const data = JSON.parse(stdout);
        for (const k of data["things"]) {
            const { thingName, thingTypeName , thingArn, version} = k;
            arr.push([thingName, thingTypeName, thingArn, version]);
        }
        if (data["NextToken"]) {
            exportThings(data["NextToken"]);
        } else {
            console.log("Exporting to things.csv")
            fs.writeFileSync("things.csv", arr.join("\n"));
            process.exit();
        }
    });
}
exportThings();
```

To run the above file use below command
```bash
    profile=sandbox node export.js
```
This file will generate the **things.csv** file as a output.