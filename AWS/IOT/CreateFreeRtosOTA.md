#### [Back](./README.md)

# Creating Free RTOS OTA.

https://gist.github.com/ahmedwahdan/144688cb73c5968bbae9abbae5107aa1

https://www.youtube.com/watch?v=HeNQZpSstss

### Create IAM User (This is uses instead of using the ROOT User)

1. Search and navigate to IAM page
2. Choose User then Add User
3. Select the name "My_OTA_User" for example
4. For access type Select whatever you like (we can use Paragmmatic access)
5. Select attach existence policy and search for and select the following
- AmazonFreeRTOSFullAccess
- AmazonFreeRTOSOTAUpdate
- AWSIoTFullAccess
6. Select Create User and download the credentials CSV file
7. Take not of the account id >> arn:aws:iam::XXXXXXXXXXXX:user/My_OTA_User
These Xs is the account id and we will need it later.

Creating Policies and Roles for OTA update/ S3 bucket access:

### Create an Amazon S3 bucket to store your update
1. Sign in to the Amazon S3 console at https://console.aws.amazon.com/s3/.
2. Choose Create bucket.
3. Enter a bucket name. (for example  testotabucket)
4. Under Bucket settings for Block Public Access keep Block all public access selected to accept the default permissions.
5. Under Bucket Versioning, select Enable to keep all versions in the same bucket.
6. Choose Create bucket.

### Create an OTA Update service role:
#### Sign in to the https://console.aws.amazon.com/iam/.
1. From the navigation pane, choose Roles.
2. Choose Create role.
3. Under Select type of trusted entity, choose AWS Service.
4. Choose IoT from the list of AWS services.
5. Under Select your use case, choose IoT.
6. Choose Next: Permissions.
7. Choose Next: Tags.
8. Choose Next: Review.
9. Enter a role name (OTA_Service_Role for example) and description, and then choose Create role.

#### Add OTA update permissions to your OTA service role:
1. Open the Role you just create (OTA_Service_Role)
2. Choose Attach policies.
3. In the Search box, enter "AmazonFreeRTOSOTAUpdate", select AmazonFreeRTOSOTAUpdate
and then choose Attach policy to attach the policy to your service role.

####  Add the required IAM permissions to your OTA service role
1. Open the Role again (OTA_Service_Role)
2. Choose Add inline policy.
3. Choose the JSON tab.
4. Copy and paste the following policy document into the text box:
```json
{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "iam:GetRole",
            "iam:PassRole"
        ],
        "Resource": "arn:aws:iam::your_account_id:role/your_role_name"
    }]
}
```
5. Update "your_account_id" with the user account you created (The Xs), and the "your_role_name" with your ota service role, which in our
example is OTA_Service_Role, so the line will be like this
"Resource": "arn:aws:iam::XXXXXXXXXXXX:role/OTA_Service_Role"
6. Choose Review policy.
7. Enter a name for the policy (for example OTA_Role_IAM_Permission_Policy), and then choose Create policy.

#### Add the required Amazon S3 permissions to your OTA service role
1. Open the Role again (OTA_Service_Role)
2. Choose Add inline policy.
3. Choose the JSON tab.
4. Copy and paste the following policy document into the text box:
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "s3:GetObjectVersion",
      "s3:GetObject",
      "s3:PutObject"
    ],
    "Resource": [
      "arn:aws:s3:::example-bucket/*"
    ]
  }]
}
```
5. Update the example-bucket with the bucket name you created, in our example testotabucket
So it will be "arn:aws:s3:::testotabucket/*"
6. Choose Review policy.
7. Enter a name for the policy (for example OTA_Role_S3_Bucket_Permission_Policy ), and then choose Create policy.

#### Create an OTA user policy:
This gives the user all the needed permission to perform OTA updates
1. In the navigation pane, choose Policies
2. Choose Create policy.
3. Choose the JSON tab, and copy and paste the following policy document into the policy editor:
```json
{
    "Version":"2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:ListBucket",
            "s3:ListAllMyBuckets",
            "s3:CreateBucket",
            "s3:PutBucketVersioning",
            "s3:GetBucketLocation",
            "s3:GetObjectVersion",
            "s3:ListBucketVersions",
            "acm:ImportCertificate",
            "acm:ListCertificates",
            "iot:*",
            "iam:ListRoles",
            "freertos:ListHardwarePlatforms",
            "freertos:DescribeHardwarePlatform"
        ],
        "Resource": "*"
    },{
        "Effect": "Allow",
        "Action": [
            "s3:GetObject",
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::example-bucket/*"
    },{   
        "Effect": "Allow",
        "Action": "iam:PassRole",
        "Resource": "arn:aws:iam::your-account-id:role/role-name"
    }]
}
```
4. Update the "example-bucket", "your-account-i", and "role-name" as before
5. Choose Review policy.
6. Enter a name for your new OTA user policy (for example OTA_User_Policy), and then choose Create policy.

#### To attach the OTA user policy to your IAM user
1. In the IAM console, in the navigation pane, choose Users, and then choose your user.
2. Choose Add permissions.
3. Choose Attach existing policies directly.
4. Search for the OTA user policy you just created (for example OTA_User_Policy) and select the check box next to it.
5. Choose Next: Review.
6. Choose Add permissions.

#### To grant your IAM user account permissions for code signing for AWS IoT
1. In the IAM console,  choose Policies.
2. Choose Create Policy.
3. On the JSON tab, copy and paste the following JSON document into the policy editor.
This policy allows the IAM user access to all code-signing operations.
```json
{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "signer:*"
        ],
        "Resource": "*"
    }]
}
```
4. Choose Review policy.
5. Enter a policy name (for example OTA_Code_Sign_Policy) and description, and then choose Create policy.
6. In the navigation pane, choose Users.
7. Choose your IAM user account.
8. On the Permissions tab, choose Add permissions.
9. Choose Attach existing policies directly, and then select the check box next to the code-signing policy you just created OTA_Code_Sign_Policy.
10. Choose Next: Review.
11. Choose Add permissions.

#### Create certificate for signing the code :
1. Download and install openssl : https://github.com/openssl/openssl/releases/tag/OpenSSL_1_1_1j
2. Add Openssl to the environment variable path
3. Create a directory and name it "Code_Certificate"
4. In your directory open command line prompt
5. Create a file named cert_config.txt. Add the following contest, Replace test_signer@amazon.com with your email address:
```bash
[ req ]
prompt             = no
distinguished_name = my_dn

[ my_dn ]
commonName = test_signer@amazon.com

[ my_exts ]
keyUsage         = digitalSignature
extendedKeyUsage = codeSigning
```
6. Create an ECDSA code-signing private key using the command:
```bash
openssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:P-256 -pkeyopt ec_param_enc:named_curve -outform PEM -out ecdsasigner.key
```
7. Create an ECDSA code-signing certificate:
```bash
openssl req -new -x509 -config cert_config.txt -extensions my_exts -nodes -days 365 -key ecdsasigner.key -out ecdsasigner.crt
```
#### Install aws cli:
- You should have python 3.4 or later installed and pip
- Install aws cli using
  pip install boto3
- Configure aws cli with your user:
  1. run command : aws configure
  2. From the CSV file you downloaded while creating the user, find access key ID, secret access key
  3. Enter access key ID, secret access key when prompt
  4. Keep Default region name [us-west-2] (just press enter)
  5. Keep Default output format [json] (just press enter)

### Now we can start

#### Prepare FreeRTOS repo and install required packages
   1. You should have python 3.4 or later installed and pip
   2. Download FreeRTOS repo and then switch to the latest release
      ```bash
      git clone https://github.com/aws/amazon-freertos.git --recurse-submodules
      git fetch --all --tags
      git checkout -f tags/202012.00 -b 202012.00-branch
      ```
   3. Go to amazon-freertos/vendors/espressif/esp-idf and in command prompt run:  install.bat
        ```bash
        cd vendors/espressif/esp-idf
        bash install.sh
        ```
        This will download and install required packages
   4. After download all packages successfully, run export.sh to populate environmental variables.

#### Create thing using aws cli and update device header files
   1. in amazon-freertos/tools/aws_config_quick_start
     open configure.json and update:
     thing_name :  to whatever name for your device, for example OTA_Device
     wifi_ssid: your wifi ssid
     wifi_password: guess what, your wifi password :D
     wifi_security: select based on your wifi router configuration
      * eWiFiSecurityOpen: Open, no security
      * eWiFiSecurityWEP: WEP security
      * eWiFiSecurityWPA: WPA security
      * eWiFiSecurityWPA2: WPA2 security   =>> Usually this option

   2. In command prompt in amazon-freertos/tools/aws_config_quick_start  run:
      python SetupAWS.py setup
      if successfully, we now include the device certificate and key in header files:
      python SetupAWS.py update_creds

#### Select OTA Demo to build,  Build and flash OTA Demo
   1. open vendors/espressif/boards/esp32/aws_demos/config_files/aws_demo_config.h
      Replace CONFIG_CORE_MQTT_MUTUAL_AUTH_DEMO_ENABLED with CONFIG_OTA_UPDATE_DEMO_ENABLED
   2. To build the demo, Open command prompt in FreeRTOS repo root and run:
      cmake -DVENDOR=espressif -DBOARD=esp32_wrover_kit -DCOMPILER=xtensa-esp32 -S . -B build -GNinja
      and for devkit
      cmake -DVENDOR=espressif -DBOARD=esp32_devkitc -DCOMPILER=xtensa-esp32 -S . -B build -GNinja
   3. To flash and monitor the demo run:
      idf.py -p COMx erase_flash flash monitor
   - Replace x in COMx with your ESP32 COM port number
   - you can use erase_flash first time only to make sure flash layout is cleaned before flash OTA demo.

#### Create OTA JOB
   1. In AWS IOT console, go to manage-> Jobs
   2. Choose create, create OTA update job
   3. Select your device, in our example "OTA_Device"
   4. Keep MQTT as the transfer protocol
   5. Select "Sign a new file for me"
   6. For Code signing profile, choose create,
       1. write the profile name, for example OTA_Sign_Profile
       2. Select device : ESP-WROVER-KIT
       3. For certificate: import the certificate and the private key that were created using openSSL
       4. For certificate path, just write /, and choose create
   7. Select your file in S3 or upload it
       1- Select your bucket, in our example: "testotabucket", and upload a file, or select previously uploaded one.
       2- OTA_Demo bin file is located in amazon-freertos/build/aws_demos.bin
       NOTE:
       The new bin file version should be higher than the one on the ESP, for example in
       amazon-freertos/demos/include/aws_application_version.h
       If the version we build and flash was 0.9.2
       We should increment the number for example to 0.9.3, and build but not flash
       using idf.py build in the FreeRTOS repo

   8. Pathname of file on device: just right /
   9. IAM role for OTA update job: choose the OTA role you created, in our examle: "OTA_Service_Role", choose Next
   10. Write and Name for the Job in ID: for exaple ID_001, then chhose create
   11. If the device is connected, Firmware update should start.
    