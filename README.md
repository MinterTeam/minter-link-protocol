### Minter Link Protocol

It describes how to represent transaction data into a simple link, which can be easily consumed by user as a link or as QR. Then link is being processed by [bip.to](https://bip.to) web app or any associated mobile app. App retrieves data from the link, generate valid transaction using logged user's private key and send it.

So everything a user needs to do to send a transaction is to click on the link or scan QR code.  

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
  Payload   []byte       // optional
  Nonce     *uint64      // optional
  GasPrice  *uint8       // optional
  GasCoin   *[10]byte    // optional
}
```

Optional fields should be kept in the RLP structure but may have value of empty list `[ 0xc0 ]`.

Data field is the same as Data of Minter transaction. It is described in the [docs](https://docs.minter.network/#section/Transactions)

- `p` - password of the check. RLP-encoded bytes array. If you want to make reedeem check link and you don't know address of recipient than you can't make check's proof. In this case you can leave Proof field empty and pass raw password in this param.

Example:
`https://bip.to/tx?d=f8bb4601018...5f8431ba0?p=83313233`

#### Native app implementation notes

Native wallet app should: 
- be associated with [bip.to](https://bip.to) website with Universal/App Links protocol;
- fallback to custom URL scheme: `minter://`, eg. `bip.to/tx?d=..` => `minter:///tx?d=..`;
