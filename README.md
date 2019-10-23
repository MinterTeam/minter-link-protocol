### Minter Link Protocol

Example:
`https://bip.to/tx?d=f8bb4601018...5f8431ba0`

- `https://bip.to` - URL
- `tx` - action

#### Params
- `d` - tx-like data. [RLP-encoded](https://github.com/ethereum/wiki/wiki/RLP) structure in hex format:
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

Optional fields should be kept in the RLP structure but may have value of empty list `[ 0xc0 ]`.

Data field is the same as Data of Minter transaction. It is described in the [docs](https://docs.minter.network/#section/Transactions)

- `p` - password of the check. RLP-encoded string. If you want to make reedeem check link and you don't know address of recipient than you can't make check's proof. In this case you can leave Proof field empty and pass raw password in this param.

Example:
`https://bip.to/tx?d=f8bb4601018...5f8431ba0?p=83313233`

#### Native app implementation notes

Native wallet app should: 
- be associated with [bip.to](https://bip.to) website with Universal/App Links protocol;
- fallback to custom URL scheme: `minter://`, eg. `bip.to/tx?d=..` => `minter:///tx?d=..`;
