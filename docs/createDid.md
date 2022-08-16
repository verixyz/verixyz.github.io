# Identifiers
When expressing statements about a specific thing, such as a person, product, or organization, it is often useful to use some kind of identifier so that others can express statements about the same thing. This specification defines the optional `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) for such identifiers. The `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) is intended to unambiguously refer to an object, such as a person, product, or organization. Using the `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) allows for the expression of statements about specific things in the [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials).

*If* the `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) is present:

- The `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *MUST* express an identifier that others are expected to use when expressing statements about a specific thing identified by that identifier.
- The `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *MUST NOT* have more than one value.
- The value of the `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *MUST* be a [URI](https://www.w3.org/TR/vc-data-model/#dfn-uri).

#### id

The value of the `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *MUST* be a single [URI](https://www.w3.org/TR/vc-data-model/#dfn-uri). It is *RECOMMENDED* that the [URI](https://www.w3.org/TR/vc-data-model/#dfn-uri) in the `id` be one which, if dereferenced, results in a document containing machine-readable information about the `id`.

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.edu/credentials/3732",
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "issuer": "https://example.edu/issuers/565049",
  "issuanceDate": "2010-01-01T00:00:00Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  }
}
```

The example above uses two types of identifiers. The first identifier is for the [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) and uses an HTTP-based URL. The second identifier is for the [subject](https://www.w3.org/TR/vc-data-model/#dfn-subjects) of the [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) (the thing the [claims](https://www.w3.org/TR/vc-data-model/#dfn-claims) are about) and uses a [decentralized identifier](https://www.w3.org/TR/vc-data-model/#dfn-decentralized-identifiers), also known as a [DID](https://www.w3.org/TR/vc-data-model/#dfn-decentralized-identifiers).

### Types

Software systems that process the kinds of objects specified in this document use type information to determine whether or not a provided [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) or [verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) is appropriate. This specification defines a `type` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) for the expression of type information.

[Verifiable credentials](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) and [verifiable presentations](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) *MUST* have a `type` [property](https://www.w3.org/TR/vc-data-model/#dfn-property). That is, any [credential](https://www.w3.org/TR/vc-data-model/#dfn-credential) or [presentation](https://www.w3.org/TR/vc-data-model/#dfn-presentations) that does not have `type` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *is not [verifiable](https://www.w3.org/TR/vc-data-model/#dfn-verify)*, so is neither a [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) nor a [verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations).

### Type

The value of the `type` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *MUST* be, or map to (through interpretation of the `@context` property), one or more [URIs](https://www.w3.org/TR/vc-data-model/#dfn-uri). If more than one [URI](https://www.w3.org/TR/vc-data-model/#dfn-uri) is provided, the [URIs](https://www.w3.org/TR/vc-data-model/#dfn-uri) *MUST* be interpreted as an unordered set. Syntactic conveniences *SHOULD* be used to ease developer usage. Such conveniences might include JSON-LD terms. It is *RECOMMENDED* that each [URI](https://www.w3.org/TR/vc-data-model/#dfn-uri) in the `type` be one which, if dereferenced, results in a document containing machine-readable information about the `type`.

With respect to this specification, the following table lists the objects that *MUST* have a [type](https://www.w3.org/TR/vc-data-model/#dfn-type) specified.

| Object                                                       | Type                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) object (a subclass of a [credential](https://www.w3.org/TR/vc-data-model/#credentials) object) | `VerifiableCredential` and, optionally, a more specific [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": ["VerifiableCredential", "UniversityDegreeCredential"]` |
| [Credential](https://www.w3.org/TR/vc-data-model/#credentials) object | `VerifiableCredential` and, optionally, a more specific [verifiable credential](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": ["VerifiableCredential", "UniversityDegreeCredential"]` |
| [Verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) object (a subclass of a [presentation](https://www.w3.org/TR/vc-data-model/#presentations) object) | `VerifiablePresentation` and, optionally, a more specific [verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": ["VerifiablePresentation", "CredentialManagerPresentation"]` |
| [Presentation](https://www.w3.org/TR/vc-data-model/#presentations) object | `VerifiablePresentation` and, optionally, a more specific [verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": ["VerifiablePresentation", "CredentialManagerPresentation"]` |
| [Proof](https://www.w3.org/TR/vc-data-model/#proofs-signatures) object | A valid proof [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": "RsaSignature2018"` |
| [credentialStatus](https://www.w3.org/TR/vc-data-model/#status) object | A valid [credential](https://www.w3.org/TR/vc-data-model/#dfn-credential) status [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": "CredentialStatusList2017"` |
| [termsOfUse](https://www.w3.org/TR/vc-data-model/#terms-of-use) object | A valid terms of use [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": "OdrlPolicy2017"`) |
| [evidence](https://www.w3.org/TR/vc-data-model/#evidence) object | A valid evidence [type](https://www.w3.org/TR/vc-data-model/#dfn-type). For example, `"type": "DocumentVerification2018"` |


## DID - decentralized identifier
DIDs are a new type of identifier that are not necessary for verifiable credentials to be useful. Specifically, verifiable credentials do not depend on DIDs and DIDs do not depend on verifiable credentials. However, it is expected that many verifiable credentials will use DIDs and that software libraries implementing this specification will probably need to resolve DIDs. DID-based URLs are used for expressing identifiers associated with subjects, issuers, holders, credential status lists, cryptographic keys, and other machine-readable information associated with a verifiable credential.

A portable URL-based identifier, also known as a DID, associated with an entity. These identifiers are most often used in a verifiable credential and are associated with subjects such that a verifiable credential itself can be easily ported from one repository to another without the need to reissue the credential. An example of a DID is `did:example:123456abcdef`.

For details about did, [W3C did-primer](https://w3c-ccg.github.io/did-primer/) is a good start point.

## Decentralized identifier document
Also referred to as a DID document, this is a document that is accessible using a verifiable data registry and contains information related to a specific `did`, such as the associated repository and public key information.

## Usage 
One could use verixyz to create, manage `did`. 

There are few `did provider` which resolve did using different method. e.g ethr is ethereum blackchain did method.

```bash
$ verixyz did create
```

The output should be like:

```bash
? Select identifier provider did:ethr
? Select key management system local
? Enter alias shanghai
┌──────────┬──────────┬───────────────────────────────────────────────────────────────────────────────┐
│ provider │    alias │                                                                           did │
├──────────┼──────────┼───────────────────────────────────────────────────────────────────────────────┤
│ did:ethr │ shanghai │ did:ethr:0x02a381fd36c91286c777a5f89e2a679b325bb25e5ca6e5e969c2f6bd09668545b2 │
└──────────┴──────────┴───────────────────────────────────────────────────────────────────────────────┘
```

One could use verixyz manage his `did`:

```bash

┌──────────────────┬───────────┬───────────────────────────────────────────────────────────────────────────────────────┐
│         provider │     alias │                                                                                   did │
├──────────────────┼───────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│          did:key │     jerry │                              did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC │
│          did:web │ jerry-web │                                                                     did:web:jerry-web │
│          did:key │      mike │                              did:key:z6MkuCdZpgX6KsNJ5wHiynLtxbjSVUvZbr4VKt46gZspyWb8 │
│         did:ethr │       kkk │         did:ethr:0x03662ceeaaa8cda843c73029ef5bac389523710ccd7ecfc4cc3f29e4c2f5e00daf │
│          did:key │       tom │                              did:key:z6Mkfof29Cr2DVyu5U7J2CVsLMrMYMiML58sREWnXmYo7C8Z │
│ did:ethr:ropsten │    7827hs │ did:ethr:ropsten:0x02391bf7a2914c2802abe1749b0bec579894be385a33dc79d5e64ae381aa3b66c8 │
│          did:web │           │                                                                              did:web: │
│ did:ethr:rinkeby │       hhh │ did:ethr:rinkeby:0x02d57e1cad723f8a60f80b894322e204fdf908cbe13b774daced5d88dc51974a58 │
│ did:ethr:rinkeby │       kkk │ did:ethr:rinkeby:0x02d3c1da9734cb22cdec7123cf6deb9ec04b4386047491ff19675ec7ce69d29624 │
│   did:ethr:kovan │           │   did:ethr:kovan:0x03dad038e392396d90a08689a4dde7f21e11b2c50bd7bb5a0e42b498c194ba9bcd │
│         did:ethr │           │         did:ethr:0x03c55d2e80cffd48edfa2d10f8e97c768d69bc0d780db824473ad6722e31f4021f │
│ did:ethr:ropsten │           │ did:ethr:ropsten:0x034d8816a8458890fdc7fdd2e405a76e71b32fab34f850da463ee38c0473325a96 │
│          did:web │ localhost │                                                                     did:web:localhost │
└──────────────────┴───────────┴───────────────────────────────────────────────────────────────────────────────────────┘
```




> NOTE: One could develop his own did method. After he add his did driver to [DIF Universal Resolver](https://dev.uniresolver.io/), then his `did` could be universal resloved.
 





