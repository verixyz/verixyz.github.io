# Verixyz Agent
The Verixyz Agent is the entry point into the Verixyz framework.

A Verixyz Agent is an implementation of an Agent using a plugin architecture. This architecture allows Verixyz to be modular, scale well and play nicely with the vast array of standards in the verifiable data space. 

## Structure of DID Agent
An Agent inclue 4 core components and customlized build blocks:
- Message
- Indetifiers
- Credentials
- Keys
- Custom(optional)

## DID Agent Function
Agent is responsible for but not limited to:
- Creating Identifiers
- Resolving Identifiers
- Credential Issuance
- Credential Revocation
- Credential Exchange
- Secret Application Hot Sauce

## Example
An Agent yaml files examples: 
 
```json
version: 3.0 

constants:
    baseUrl: http://localhost:3332
    port: 3332
    dbEncryptionKey: xxx //a X25519 key, generate a new key by running `
    databaseFile: ./database.sqlite
    metholds: //selected from plugins

        - keyManagerCreate
        - handleMessage
        - ...

# Database 
dbconnection:
  $require: typeorm?t=function#createConnection
  $args:
        - type: sqlite
      database:
        $ref: /constants/databaseFile
      synchronize: false
      migrationsRun: true
      migrations:
        $require: '@verixyz/data-store?t=object#migrations'
      logging: false
      entities:
        $require: '@verixyz/data-store?t=object#Entities'

# Server Config
...
```

Metholds defined in plugins are available on the Agent instance. e.g.
```js
const message = await agent.handleMessage({
    raw: 'thwrthrtrtnwrtnwertetnrth.qaerthq.erth.erth.eTR.Heth'
})
```


