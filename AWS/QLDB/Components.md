#### [Back](./README.md)

# AWS QLDB Components

1. **Current State:-** Current State is nothing but traditional database with the latest data.

2. **History Data:-** In history data different versions of a particular unit of data is stored. For every update a new version is created and added to history data.

3. **Journal:-** To maintain an immutable copy of all the changes history data is linked using SHA256 hash of data making the history cryptographically verifiable.