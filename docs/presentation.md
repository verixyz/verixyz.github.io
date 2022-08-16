### Presentations

[Presentations](https://www.w3.org/TR/vc-data-model/#dfn-presentations) *MAY* be used to combine and present [credentials](https://www.w3.org/TR/vc-data-model/#dfn-credential). They can be packaged in such a way that the authorship of the data is [verifiable](https://www.w3.org/TR/vc-data-model/#dfn-verify). The data in a [presentation](https://www.w3.org/TR/vc-data-model/#dfn-presentations) is often all about the same [subject](https://www.w3.org/TR/vc-data-model/#dfn-subjects), but there is no limit to the number of [subjects](https://www.w3.org/TR/vc-data-model/#dfn-subjects) or [issuers](https://www.w3.org/TR/vc-data-model/#dfn-issuers) in the data. The aggregation of information from multiple [verifiable credentials](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) is a typical use of [verifiable presentations](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations).

A [verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) is typically composed of the following properties:

- id

  The `id` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) is optional and *MAY* be used to provide a unique identifier for the [presentation](https://www.w3.org/TR/vc-data-model/#dfn-presentations). For details related to the use of this property, see Section [4.2 Identifiers](https://www.w3.org/TR/vc-data-model/#identifiers).

- type

  The `type` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) is required and expresses the type of [presentation](https://www.w3.org/TR/vc-data-model/#dfn-presentations), such as `VerifiablePresentation`. For details related to the use of this property, see Section [4.3 Types](https://www.w3.org/TR/vc-data-model/#types).

- verifiableCredential

  If present, the value of the `verifiableCredential` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) *MUST* be constructed from one or more [verifiable credentials](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials), or of data derived from [verifiable credentials](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials) in a cryptographically [verifiable](https://www.w3.org/TR/vc-data-model/#dfn-verify) format.

- holder

  If present, the value of the `holder` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) is expected to be a [URI](https://www.w3.org/TR/vc-data-model/#dfn-uri) for the entity that is generating the [presentation](https://www.w3.org/TR/vc-data-model/#dfn-presentations).

- proof

  If present, the value of the `proof` [property](https://www.w3.org/TR/vc-data-model/#dfn-property) ensures that the [presentation](https://www.w3.org/TR/vc-data-model/#dfn-presentations) is [verifiable](https://www.w3.org/TR/vc-data-model/#dfn-verify). For details related to the use of this property, see Section [4.7 Proofs (Signatures)](https://www.w3.org/TR/vc-data-model/#proofs-signatures).

The example below shows a [verifiable presentation](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-presentations) that embeds [verifiable credentials](https://www.w3.org/TR/vc-data-model/#dfn-verifiable-credentials).

```bash
$ verixyz presentation
```


```bash
Holder DID did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC jerry
? Tag (threadId) xyz123
? Verifier DID did:key:z6Mkfof29Cr2DVyu5U7J2CVsLMrMYMiML58sREWnXmYo7C8Z
? Presentation type VerifiablePresentation,Profile
? Select credential {"bankaccount":"9829-92839-2923","id":"did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC"} | Issuer: 
did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC
? Add another credential? No
{
  tag: 'xyz123',
  verifiableCredential: [
    {
      credentialSubject: {
        bankaccount: '9829-92839-2923',
        id: 'did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC'
      },
      issuer: {
        id: 'did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC'
      },
      type: [ 'VerifiableCredential', 'Profile' ],
      credentialStatus: {
        type: 'EthrStatusRegistry2019',
        id: 'rinkeby:0x97fd27892cdcD035dAe1fe71235c636044B59348'
      },
      '@context': [
        'https://www.w3.org/2018/credentials/v1',
        'https://verixyz.io/contexts/profile/v1'
      ],
      issuanceDate: '2022-08-15T23:16:12.000Z',
      proof: {
        type: 'JwtProof2020',
        jwt: 'eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9.eyJ2YyI6eyJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvMjAxOC9jcmVkZW50aWFscy92MSIsImh0dHBzOi8vdmVyaXh5ei5pby9jb250ZXh0cy9wcm9maWxlL3YxIl0sInR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJQcm9maWxlIl0sImNyZWRlbnRpYWxTdWJqZWN0Ijp7ImJhbmthY2NvdW50IjoiOTgyOS05MjgzOS0yOTIzIn0sImNyZWRlbnRpYWxTdGF0dXMiOnsidHlwZSI6IkV0aHJTdGF0dXNSZWdpc3RyeTIwMTkiLCJpZCI6InJpbmtlYnk6MHg5N2ZkMjc4OTJjZGNEMDM1ZEFlMWZlNzEyMzVjNjM2MDQ0QjU5MzQ4In19LCJzdWIiOiJkaWQ6a2V5Ono2TWtrWktNdVBuNWM0YmZqdHhrcW1MY3ZZdEM2RmFUMWFXQ2hBeWhQTUZTWUh3QyIsIm5iZiI6MTY2MDYwNTM3MiwiaXNzIjoiZGlkOmtleTp6Nk1ra1pLTXVQbjVjNGJmanR4a3FtTGN2WXRDNkZhVDFhV0NoQXloUE1GU1lId0MifQ.LGNpgVFjFuAs9-aHUZz3HYQD9NRtIcibdjkQ6wOZLJWp_FnHfhKyudon6LQUfZQSv7QtQc37l-Z5ODTCcyb1DQ'
      }
    }
  ],
  holder: 'did:key:z6MkkZKMuPn5c4bfjtxkqmLcvYtC6FaT1aWChAyhPMFSYHwC',
  verifier: [ 'did:key:z6Mkfof29Cr2DVyu5U7J2CVsLMrMYMiML58sREWnXmYo7C8Z' ],
  type: [ 'VerifiablePresentation', 'Profile' ],
  '@context': [ 'https://www.w3.org/2018/credentials/v1' ],
  issuanceDate: '2022-08-15T23:59:11.000Z',
  proof: {
    type: 'JwtProof2020',
    jwt: 'eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9.eyJ2cCI6eyJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvMjAxOC9jcmVkZW50aWFscy92MSJdLCJ0eXBlIjpbIlZlcmlmaWFibGVQcmVzZW50YXRpb24iLCJQcm9maWxlIl0sInZlcmlmaWFibGVDcmVkZW50aWFsIjpbImV5SmhiR2NpT2lKRlpFUlRRU0lzSW5SNWNDSTZJa3BYVkNKOS5leUoyWXlJNmV5SkFZMjl1ZEdWNGRDSTZXeUpvZEhSd2N6b3ZMM2QzZHk1M015NXZjbWN2TWpBeE9DOWpjbVZrWlc1MGFXRnNjeTkyTVNJc0ltaDBkSEJ6T2k4dmRtVnlhWGg1ZWk1cGJ5OWpiMjUwWlhoMGN5OXdjbTltYVd4bEwzWXhJbDBzSW5SNWNHVWlPbHNpVm1WeWFXWnBZV0pzWlVOeVpXUmxiblJwWVd3aUxDSlFjbTltYVd4bElsMHNJbU55WldSbGJuUnBZV3hUZFdKcVpXTjBJanA3SW1KaGJtdGhZMk52ZFc1MElqb2lPVGd5T1MwNU1qZ3pPUzB5T1RJekluMHNJbU55WldSbGJuUnBZV3hUZEdGMGRYTWlPbnNpZEhsd1pTSTZJa1YwYUhKVGRHRjBkWE5TWldkcGMzUnllVEl3TVRraUxDSnBaQ0k2SW5KcGJtdGxZbms2TUhnNU4yWmtNamM0T1RKalpHTkVNRE0xWkVGbE1XWmxOekV5TXpWak5qTTJNRFEwUWpVNU16UTRJbjE5TENKemRXSWlPaUprYVdRNmEyVjVPbm8yVFd0cldrdE5kVkJ1TldNMFltWnFkSGhyY1cxTVkzWlpkRU0yUm1GVU1XRlhRMmhCZVdoUVRVWlRXVWgzUXlJc0ltNWlaaUk2TVRZMk1EWXdOVE0zTWl3aWFYTnpJam9pWkdsa09tdGxlVHA2TmsxcmExcExUWFZRYmpWak5HSm1hblI0YTNGdFRHTjJXWFJETmtaaFZERmhWME5vUVhsb1VFMUdVMWxJZDBNaWZRLkxHTnBnVkZqRnVBczktYUhVWnozSFlRRDlOUnRJY2liZGprUTZ3T1pMSldwX0ZuSGZoS3l1ZG9uNkxRVWZaUVN2N1F0UWMzN2wtWjVPRFRDY3liMURRIl19LCJ0YWciOiJ4eXoxMjMiLCJuYmYiOjE2NjA2MDc5NTEsImlzcyI6ImRpZDprZXk6ejZNa2taS011UG41YzRiZmp0eGtxbUxjdll0QzZGYVQxYVdDaEF5aFBNRlNZSHdDIiwiYXVkIjpbImRpZDprZXk6ejZNa2ZvZjI5Q3IyRFZ5dTVVN0oyQ1ZzTE1yTVlNaU1MNThzUkVXblhtWW83QzhaIl19.y2p4-36Kh5rdOCA2nrgHf4VKDDDbvwfWka2Tz3mDA8j4PB0r_6C5muxbqlq-MOK65xwwS0aMXzs-ZV2dz94WDQ'
  }
}
```
