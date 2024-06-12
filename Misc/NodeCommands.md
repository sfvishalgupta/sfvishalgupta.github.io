#### [Back](./README.md)

# Node Commands

* #### Get Path of Global Node Modules folder
```shell
npm root -g

OR

npm config get prefix
```

* #### To Edit Global module path
```shell
npm config edit
prefix = /my/npm/global/modules/prefix ## Puth this value in config file.

OR 

npm config set prefix /my/npm/global/modules/prefix
```

* #### Global Module List
```shell
npm list -g --depth=0
```