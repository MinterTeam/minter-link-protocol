### Minter Link Protocol

Example:
`https://bip.to/tx?d=f8bb4601018...5f8431ba0`

- `https://bip.to` - URL
- `tx` - action

#### Actions

Action: 
- `tx`

Params: 
- `d` - data. [RLP-encoded](https://github.com/ethereum/wiki/wiki/RLP) structure in hex format:
```golang
type Data struct {  
  Type      byte
  Data      []byte
  Payload   []byte
  
  Nonce     *int      // optional
  GasPrice  *int      // optional
  GasCoin   *[10]byte // optional
}
```

Optional field should be kept in the RLP structure but may have value of empty list `[ 0xc0 ]`.

#### Native app implementation notes

Native wallet app should: 
- be associated with bip.to website with Universal/App Links protocol;
- fallback to custom URL scheme: `minter://`, eg. `bip.to/tx?d=..` => `minter:///tx?d=..`;
