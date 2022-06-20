# Plugins
Addtional functionality in Verixyz is added to the `Agent` via the plugin system. 

One can writing and configuraing pligin by their custom needs when builiding applications on Verixyz. Custom plugins can just live in a directory, private repository or on npm packages where can be shared with others. 

Verixyz community encourage developers to follow some basic rules when writing/devolping plugins to ensure the whole ecosystem of highly interoperable functions.

## Plugins Architecture

```mermaid
classDiagram
    Verixyz Agent <|-- IKeyManager
    Verixyz Agent <|-- IDataStore
    Verixyz Agent <|-- IDIDManager
    Verixyz Agent <|-- IResolver
    Verixyz Agent <|-- ICredentialIssuer
    Verixyz Agent : Messages
    Verixyz Agent : Identifiers
    Verixyz Agent : Credentials
    Verixyz Agent : Keys
    Verixyz Agent : Custom
    class IKeyManager{
        KMS{local,vault}
        KeyStore
    }
    class IDataStore{
        DBConnection{postgres}
    }
    class IDIDManager{
        DIDStore
        DIDProviders{WebDIDProvder,ethDIDProvider,keyProvider}
    }
    class IResolver{
        Resolver{WebDIDResolver}
    }
    class ICredentialIssuer{
        JWT
    }
```

## Plugins API 
All the plugins API reference should be seen on npmjs. 

[@verixyz/core#](https://www.npmjs.com/package/@verixyz/core)


[@verixyz/did-manager#](https://www.npmjs.com/package/@verixyz/did-manager)


[@verixyz/did-provider-ethr#](https://www.npmjs.com/package/@verixyz/did-provider-ethr)


[@verixyz/did-provider-web#](https://www.npmjs.com/package/@verixyz/did-provider-web)


[@verixyz/did-provider-key#](https://www.npmjs.com/package/@verixyz/did-provider-key)


[@verixyz/key-manager#](https://www.npmjs.com/package/@verixyz/key-manager)


[@verixyz/kms-local#](https://www.npmjs.com/package/@verixyz/kms-local)


[@verixyz/did-resolver#](https://www.npmjs.com/package/@verixyz/did-resolver)


[@verixyz/did-comm#](https://www.npmjs.com/package/@verixyz/did-comm)


[@verixyz/did-jwt#](https://www.npmjs.com/package/@verixyz/did-jwt)


[@verixyz/message-handler#](https://www.npmjs.com/package/@verixyz/message-handler)


[@verixyz/url-handler#](https://www.npmjs.com/package/@verixyz/url-handler)


[@verixyz/selective-disclosure#](https://www.npmjs.com/package/@verixyz/selective-disclosure)


[@verixyz/credential-w3c#](https://www.npmjs.com/package/@verixyz/credential-w3c)


[@verixyz/remote-server#](https://www.npmjs.com/package/@verixyz/remote-server)


[@verixyz/data-store#](https://www.npmjs.com/package/@verixyz/data-store)


[@verixyz/remote-client#](https://www.npmjs.com/package/@verixyz/remote-client)

    


