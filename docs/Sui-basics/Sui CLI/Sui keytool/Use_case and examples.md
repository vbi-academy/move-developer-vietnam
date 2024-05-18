---

---


# Use cases and example: sui keytool 
Responsible for managing the address and private key used by the SUI client

If you already have a mnemonic phrase and want to import it to the SUI client, you can use the following command from the SUI Keytool.


## Generate new address 
When you use Sui libraries, you need a keypair. Keypairs help to make things more secure and are created using special math procedures called cryptographic algorithms. 

Some of these algorithms are Ed25519, ECDSA Secp256k1, and ECDSA Secp256r1. They help keep your data safe and confirm your identity, which makes using Sui libraries secure and easy.

```Bash
# Create ED25519 keypair scheme
sui client new-address ed25519

# Create SECP256K1 keypair scheme
sui client new-address secp256k1

# Create SECP256R1 keypair scheme
sui client new-address secp256r1
```

The output with details about the newly generated address:

![Sui client new-address](/img/Sui-client/keytool/generate_address.png)
