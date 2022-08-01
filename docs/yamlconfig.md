# YAML Configuration
Verixyz-cli uses a YAML file for configuration. 

Objects are created by a helper function `createObjects`, which recursively mutates the configuration object that was parsed from a YAML file and applies custom rules for objects containing:

- Module imports
```yaml
{
  "$require": "path...",
  "$args": {}
}
```
- Object references
```yaml
{
  "$ref": "/yaml/pointer"
}
```
- Environment variables
```yaml
{
  "$env": "ENV_VAR"
}
```
## Requiring npm modules
This:
```js
import { Agent } from '@verixyz/core'
import { DIDComm } from '@verixyz/did-comm'
const agent = new Agent({
  plugins: [new DIDComm()],
})
```
is equivalent to:
```js
const agent = new (require('@verixyz/core')['Agent'])({
  plugins: [new (require('@verixyz/core')['DIDComm'])()],
})
```
which is equivalent to:
```yaml
agent:
  $require: '@verixyz/core#Agent'
  $args:
    - plugins:
        - $require: '@verixyz/did-comm#DIDComm'
```

### $require syntax
ethr-did-resolver?t=function&p=/ethr#getResolver
- ethr-did-resolver - Module name
- t=function - Optional. Type can be function, object, class. Default is class
    - class - imported symbol will be initiated with new symbolName(args)
    - function - imported symbol will be initiated with symbolName(args)
    - object - imported object will be returned without aditional processing
- p=/ethr - Optional. Pointer to an attribute in imported symbol
- #getResolver - Imported symbol name

```yaml
result:
  $require: 'ethr-did-resolver?t=function&p=/ethr#getResolver'
  $args:
    - networks:
        - name: mainnet
          rpcUrl: https://mainnet.infura.io/v3/5ffc47f65c4042ce847ef66a3fa70d4c
        - name: rinkeby
          rpcUrl: https://rinkeby.infura.io/v3/5ffc47f65c4042ce847ef66a3fa70d4c
```

is equivalent to:
```js
import { getResolver } from 'ethr-did-resolver'
const obj = getResolver({
  networks: [
    {
      name: 'mainnet',
      rpcUrl: 'https://mainnet.infura.io/v3/5ffc47f65c4042ce847ef66a3fa70d4c',
    },
    {
      name: 'rinkeby',
      rpcUrl: 'https://rinkeby.infura.io/v3/5ffc47f65c4042ce847ef66a3fa70d4c',
    },
  ],
})

const result = obj.ethr
```

### Referencing objects ( $ref )
```yaml
agent:
  $require: '@verixyz/core#Agent'
  $args:
    - plugins:
        - $require: '@verixyz/did-comm#DIDComm'
```
is equivalent to:
```yaml
didComm:
  $require: '@verixyz/did-comm#DIDComm'

agent:
  $require: '@verixyz/core#Agent'
  $args:
    - plugins:
        - $ref: /didComm
```

By referencing objects you can ensure that only one copy of the object is created in memory and can be shared by different modules. For example the same database connection used by different plugins:
```yaml
dbConnection:
  $require: 'typeorm?t=function#createConnection'
  $args:
    - type: 'sqlite'
      database:
        $env: 'DATABASE_FILE'
      entities:
        $require: '@verixyz/data-store?t=object#Entities'

agent:
  $require: '@verixyz/core#Agent'
  $args:
    - schemaValidation: false
      plugins:
        - $require: '@verixyz/data-store#DataStore'
          $args:
            - $ref: /dbConnection
        - $require: '@verixyz/data-store#DataStoreORM'
          $args:
            - $ref: /dbConnection
```
## Server
Example:
```yaml
server:
  baseUrl: 'http://localhost:3332'
  port: '3332'

  # Array of express middleware
  use:
    # CORS
    - - $require: 'cors?t=function'

    # Add agent to the request object
    - - $require: '@verixyz/remote-server?t=function#RequestWithAgentRouter'
        $args:
          - agent:
              $ref: /agent

  # Execute during server initialization
  init:
    - $require: '@verixyz/remote-server?t=function#createDefaultDid'
      $args:
        - agent:
            $ref: /agent
          baseUrl:
            $ref: /constants/baseUrl
          messagingServiceEndpoint: /messaging
```

`server.use` is an array of expressjs middleware arrays

`server.init` is an array of functions that need to be run during server initialization

