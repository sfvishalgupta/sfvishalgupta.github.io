#### [Back](./README.md)

# Bash Script to Create Multiple AWS Things

Prerequisites of creating multiple things at once.

1. Proper aws cli setup.
2. Certificate already created via IOT Core.
3. You should have permission to create things via CLI.

**Below is the bash script to create multiple things and register via certificate.**

```bash
#! /bin/bash
for i in {1..400}
do
    aws iot create-thing --thing-type-name IF31 --thing-name PNR01ABC1000$i
    aws iot attach-thing-principal --principal $1 --thing-name PNR01ABC1000$i
done
```

**Below is the command to run the above script considering file name is createThing.sh**

```bash
bash ./createThings.sh arn_of_certificate
```

The above script will create 400 devices and register on one certificate whos ARN is provided via CLI.