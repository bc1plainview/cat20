# FAIR CAT-20: A Fair Experimental Bitcoin Token Standard Leveraging OP_CAT &amp; Ordinal Consensus

Welcome to the official documentation for **CAT-20**, an innovative and experimental metaprotocol standard for fungible tokens on the Bitcoin blockchain. This version of CAT-20, created by Twitter user [@bc1plainview](https://twitter.com/bc1plainview), predates the newer CAT-20 standard by sCrypt by one month. Inspired by BRC-20 and rooted in Ordinals, this experimental CAT-20 introduces the use of Bitcoin's `OP_CAT` opcode to streamline token creation and management.

**Note**: This CAT-20 is purely experimental and will only be operational on Fractal Mainnet after block 21,000. As such, anyone is free to build an indexer for it, and it operates similarly to BRC-20 in terms of minting, deploying, and transferring tokens via Ordinal inscriptions.

For more information on the newer CAT-20 standard created by sCrypt, you can check out **ProtocolCAT**. However, this document will focus solely on the experimental CAT-20 designed by bc1plainview, which is based on Ordinals and should feel familiar to users accustomed to BRC-20.

---

## What is CAT-20?

CAT-20 is a cutting-edge token standard specifically designed for Bitcoin, leveraging the powerful capabilities of the `OP_CAT` opcode to handle token operations more efficiently. With CAT-20, token creation, minting, and transferring are all performed directly within Bitcoin’s script language, minimizing off-chain dependencies and ensuring efficient on-chain operations.

This experimental version of CAT-20 is fully compatible with Bitcoin's Ordinal system, meaning that deploying, minting, and transferring tokens is as simple as creating Ordinal inscriptions, just like with BRC-20 tokens.

---

## Why CAT-20?

CAT-20 introduces several key advantages over previous standards, such as BRC-20:

- **Efficiency**: Using `OP_CAT`, CAT-20 can concatenate and manage token data directly within Bitcoin’s script, reducing the need for off-chain processing and allowing for more efficient transactions.
- **Flexibility**: CAT-20 scripts dynamically build and execute token operations, offering more versatility and control over how tokens are managed.
- **Integration**: CAT-20 operates natively on the Bitcoin blockchain while introducing new capabilities through Bitcoin’s scripting language and the `OP_CAT` opcode.

---

## The Power of OP_CAT in CAT-20

At the heart of CAT-20 is the `OP_CAT` opcode, a critical tool that allows the concatenation of two values on the Bitcoin stack. This capability is essential for constructing efficient token operations within a single Bitcoin transaction.

### How OP_CAT Works:

1. **Pushing Values to the Stack**: The script pushes various components of the token operation (e.g., protocol identifier, operation type, ticker, etc.) onto the stack.
2. **Concatenation with OP_CAT**: `OP_CAT` pops the top two items from the stack, concatenates them, and pushes the result back onto the stack. This process is repeated for each element, gradually building the final operation string.
3. **Final Output**: The final output is a concatenated string that represents the token operation (e.g., deployment, minting, or transferring), which is then inscribed on the blockchain.

---

## Example: Deploying a CAT-20 Token

Let’s walk through a simple example to demonstrate the power of `OP_CAT` in a CAT-20 token deployment. In this case, we will deploy a CAT-20 token called **CAT** with a maximum supply of 210,000,000 tokens, a mint limit of 1 token per inscription, and 8 decimal places.

### Deployment Script:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 deploy operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "deploy:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "210000000,"
    OP_CAT

    OP_PUSH "lim=1,"
    OP_CAT

    OP_PUSH "dec=8"
    OP_CAT

    # End of CAT-20 deploy operation
OP_ENDIF
```

### Concatenated Output:

```plaintext
"cat20:deploy:CAT=210000000,lim=1,dec=8"
```

This script showcases the efficiency and simplicity of CAT-20. Each component of the deployment is pushed to the stack and concatenated using `OP_CAT`, resulting in a fully-formed deployment string that is inscribed on the Bitcoin blockchain.

---

## Experimental Nature of CAT-20

This version of CAT-20 is experimental, and its full functionality will only be available after block 21,000 on the Fractal Mainnet. As an open standard, anyone can create an indexer for CAT-20 tokens, making it a highly flexible and community-driven protocol. Since CAT-20 is based on Ordinals, users familiar with BRC-20 will find the process of minting, deploying, and transferring tokens straightforward and familiar.

Keep in mind that this CAT-20 is purely for experimentation and development purposes. It provides the opportunity for the Bitcoin community to explore new ways of handling fungible tokens on Bitcoin using `OP_CAT`, while maintaining the simplicity and compatibility of the Ordinals system.

---

## Conclusion

CAT-20 represents a significant step forward in how tokens can be managed on Bitcoin. By incorporating the `OP_CAT` opcode, CAT-20 simplifies token operations, reduces reliance on off-chain systems, and enhances Bitcoin’s native scripting capabilities. As an experimental protocol, it is open for developers and enthusiasts to test, modify, and build indexers.

In the following sections, we will explore how to deploy, mint, and transfer CAT-20 tokens, as well as the specific rules that govern the CAT-20 metaprotocol. Stay tuned as we delve deeper into the world of CAT-20, where efficiency and innovation meet on the Bitcoin blockchain.

# CAT-20 Token Operations: Deploying, Minting, and Transferring

In this section, we’ll walk through the detailed process of deploying, minting, and transferring CAT-20 tokens on the Bitcoin blockchain. Each operation leverages the power of the `OP_CAT` opcode within the Ordinal Envelope to ensure efficient and streamlined execution. Whether you’re creating a new token or managing an existing one, these instructions will guide you through the steps.

---

## 1. Deploying a CAT-20 Token

The deployment process initializes a new CAT-20 token with specific parameters like the ticker, maximum supply, mint limit, and decimal precision. Here’s how to deploy a CAT-20 token:

### Script for Deploying a CAT-20 Token:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 deploy operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "deploy:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "210000000,"
    OP_CAT

    OP_PUSH "lim=1,"
    OP_CAT

    OP_PUSH "dec=8"
    OP_CAT

    # End of CAT-20 deploy operation
OP_ENDIF
```

### Final Concatenated String:

```plaintext
"cat20:deploy:CAT=210000000,lim=1,dec=8"
```

### Explanation:

- `"cat20:"`: Specifies the protocol and identifies it as a CAT-20 token.
- `"deploy:"`: Indicates that this is a deploy operation.
- `"CAT="`: The ticker for the token.
- `"210000000,"`: The maximum supply for the token.
- `"lim=1,"`: The mint limit per wallet.
- `"dec=8"`: The number of decimals for the token.

Once this script is inscribed on the Bitcoin blockchain, it creates a new CAT-20 token with the specified parameters.

---

## 2. Minting CAT-20 Tokens

Minting creates new tokens within the limits set during deployment. The first wallet to inscribe a mint operation will receive the specified amount of tokens.

### Script for Minting CAT-20 Tokens:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 mint operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "mint:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "1"
    OP_CAT

    # End of CAT-20 mint operation
OP_ENDIF
```

### Final Concatenated String:

```plaintext
"cat20:mint:CAT=1"
```

### Explanation:

- `"mint:"`: Indicates that this is a mint operation.
- `"CAT="`: The ticker for the token.
- `"1"`: The number of tokens to be minted.

This script mints 1 CAT token to the wallet that inscribes this operation. The minting process respects the limits set during the deployment.

---

## 3. Transferring CAT-20 Tokens

Transferring CAT-20 tokens involves moving a specified amount from one wallet to another. The transfer script ensures that the correct amount is deducted from the sender’s balance and added to the receiver’s balance.

### Script for Transferring CAT-20 Tokens:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 transfer operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "transfer:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "5"
    OP_CAT

    # End of CAT-20 transfer operation
OP_ENDIF
```

### Final Concatenated String:

```plaintext
"cat20:transfer:CAT=5"
```

### Explanation:

- `"transfer:"`: Indicates that this is a transfer operation.
- `"CAT="`: The ticker for the token.
- `"5"`: The amount of tokens to be transferred.

When this script is executed, 5 CAT tokens are transferred from the sender’s wallet to the receiver’s wallet.

---

## Summary

Deploying, minting, and transferring CAT-20 tokens are all managed through Bitcoin’s script language, enhanced by the `OP_CAT` opcode. Each operation concatenates its respective components into a final string that represents the action on-chain. This method not only leverages Bitcoin’s existing infrastructure but also introduces a level of efficiency and simplicity that makes CAT-20 a powerful tool for token management on the Bitcoin blockchain.

In the next section, we will dive into the specific rules and guidelines that govern the CAT-20 metaprotocol, ensuring consistent and reliable operation across the network.

# Practical Examples: Deploying, Minting, and Transferring CAT-20 Tokens

In this section, we'll provide practical, hands-on examples of how to deploy, mint, and transfer CAT-20 tokens on the Bitcoin blockchain. These examples will guide you through the process step by step, using the scripts and rules outlined in the previous sections.

---

## 1. Deploying a CAT-20 Token

Let’s start with an example of deploying a new CAT-20 token called **CAT** with a maximum supply of 210,000,000 tokens, a mint limit of 1,000 tokens per inscription, and 8 decimal places.

### Deployment Script:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 deploy operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "deploy:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "210000000,"
    OP_CAT

    OP_PUSH "lim=1,"
    OP_CAT

    OP_PUSH "dec=8"
    OP_CAT

    # End of CAT-20 deploy operation
OP_ENDIF
```

### Final Concatenated String:

```plaintext
"cat20:deploy:CAT=210000000,lim=1,dec=8"
```

### Outcome:

This deployment script initializes a new CAT-20 token with the ticker **CAT**, a maximum supply of 210,000,000 tokens, a mint limit of 1,000 per inscription, and 8 decimal places. The script is inscribed on the blockchain, making the CAT token officially deployed and available for minting.

---

## 2. Minting CAT-20 Tokens

Once a token is deployed, you can mint additional tokens up to the maximum supply defined during deployment. In this example, we’ll mint 1,000 CAT tokens.

### Minting Script:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 mint operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "mint:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "1"
    OP_CAT

    # End of CAT-20 mint operation
OP_ENDIF
```

### Final Concatenated String:

```plaintext
"cat20:mint:CAT=1"
```

### Outcome:

This minting script creates 1,000 CAT tokens and assigns them to the first wallet that inscribes this operation. This operation respects the mint limit of 1,000 tokens per inscription, as specified during deployment.

---

## 3. Transferring CAT-20 Tokens

After minting, you may want to transfer tokens to another wallet. In this example, we’ll transfer 500 CAT tokens from one wallet to another.

### Transfer Script:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 transfer operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "transfer:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "5"
    OP_CAT

    # End of CAT-20 transfer operation
OP_ENDIF
```

### Final Concatenated String:

```plaintext
"cat20:transfer:CAT=5"
```

### Outcome:

This transfer script moves 500 CAT tokens from the sender’s wallet to the receiver’s wallet. The script ensures that the correct amount is deducted from the sender's balance and added to the receiver's balance upon completion of the transfer.

---

## 4. Advanced Example: Combined Operations

For users who wish to perform multiple operations in a single script, CAT-20 allows for flexibility. Here’s an example of minting and then immediately transferring 200 CAT tokens to another wallet.

### Combined Mint and Transfer Script:

```bash
OP_FALSE OP_IF
    OP_PUSH "ord"                  # Ordinal magic code
    OP_PUSH 1                      # Version number
    OP_PUSH "text/plain;charset=utf-8"  # MIME type
    OP_PUSH 0                      # Push 0 to signal start of data

    # Begin CAT-20 mint operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "mint:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "1"
    OP_CAT

    # Begin CAT-20 transfer operation
    OP_PUSH "cat20:"
    OP_CAT

    OP_PUSH "transfer:"
    OP_CAT

    OP_PUSH "CAT="
    OP_CAT

    OP_PUSH "2"
    OP_CAT

    # End of CAT-20 operations
OP_ENDIF
```

### Final Concatenated Strings:

- **Minting Operation**: `"cat20:mint:CAT=1"`
- **Transfer Operation**: `"cat20:transfer:CAT=2"`

### Outcome:

This combined script first mints 200 CAT tokens and then immediately transfers them to another wallet. This example demonstrates the flexibility of CAT-20 scripts, allowing multiple operations to be chained together in a single transaction.

---

## Conclusion

These practical examples provide a clear roadmap for using CAT-20 tokens on the Bitcoin blockchain. By following these scripts, you can confidently deploy, mint, and transfer tokens, taking full advantage of the power and flexibility offered by the `OP_CAT` opcode.

Whether you’re a developer, a token creator, or simply exploring the possibilities of CAT-20, these examples will serve as your guide to executing token operations efficiently and effectively. As CAT-20 continues to evolve, so too will the strategies and best practices for managing tokens on Bitcoin, opening up new opportunities for innovation and growth.

# CAT-20 Rules and Guidelines

The CAT-20 standard is governed by a set of rules and guidelines that ensure consistent behavior, compatibility, and security across the Bitcoin network. Understanding these rules is essential for anyone looking to deploy, mint, or transfer CAT-20 tokens. This section outlines the key rules and best practices to follow when working with CAT-20 tokens.

---

## 1. Ticker Uniqueness and Case Sensitivity

- **Uniqueness**: The ticker symbol for a CAT-20 token must be unique. The first deployment of a ticker on the blockchain is the only one recognized by the network.
- **Case Insensitivity**: Ticker symbols are case-insensitive. For example, CAT, cat, and Cat are considered the same ticker. Deploying multiple tickers with different cases is not allowed.

---

## 2. Maximum Supply and Mint Limits

- **Maximum Supply**: The maximum supply of a CAT-20 token must be defined during the deployment. This value cannot exceed `uint64_max` (18,446,744,073,709,551,615).
- **Mint Limit**: An optional mint limit can be set during deployment, specifying the maximum number of tokens that can be minted in a single operation. This helps prevent over-minting and ensures fair distribution.

---

## 3. Decimal Precision

- **Decimal Precision**: CAT-20 tokens can specify a decimal precision up to 18 decimal places. The number of decimals is defined during deployment and cannot be changed later. The default is 18 if not specified.

---

## 4. Token Operations and Balance Management

- **Deploy**: The deploy operation initializes a CAT-20 token with the specified parameters. It does not affect the token balance or state directly.
- **Mint**: The mint operation adds tokens to the balance of the first owner of the mint inscription. Mint operations must respect the mint limit and maximum supply defined during deployment.
- **Transfer**: The transfer operation moves tokens from one wallet to another. The amount specified in the transfer must not exceed the sender's available balance.

### Transfer Validation and Redundancies

- **Valid Transfer Functions**: A transfer function is valid if the amount being transferred does not exceed the available balance at the time of inscription. The available balance is calculated as:  
  `Available Balance = Overall Balance - Valid Transferable Balance`
- **Redundant Transfers**: If a user no longer wishes to complete a transfer, they can invalidate the transfer by sending the transfer inscription back to themselves. This restores the available balance to its original state.

---

## 5. Order of Operations and Block Confirmation

- **Order of Confirmation**: If multiple operations occur within the same block, their order of confirmation is determined by the sequence in which they are confirmed within the block. Earlier confirmations take precedence.
- **Block-Level Priority**: In cases where operations are confirmed in the same block, the first operation confirmed will be prioritized. This ensures that operations are processed in the correct order.

---

## 6. Inscriptions and Transaction Fees

- **Inscriptions**: CAT-20 operations are inscribed on the Bitcoin blockchain using the Ordinal Envelope format, combined with `OP_CAT` for concatenation. These inscriptions must be correctly formatted to be valid.
- **Transaction Fees**: No valid CAT-20 operation can occur via spending an ordinal through a transaction fee. If a fee payment is involved during the inscription process, the resulting inscription is ignored. If it occurs during the transfer process, the balance is returned to the sender's available balance.

---

## 7. Security and Best Practices

- **Security**: Always ensure that inscriptions are sent to a wallet that supports Ordinals and the CAT-20 protocol. Sending to non-compatible wallets may result in loss of tokens.

### Best Practices:

- **Minting**: Always inscribe mint operations directly to your own wallet to avoid third-party interference.
- **Transferring**: Ensure that the transfer function is valid and that the receiving address holds a compatible wallet before completing a transfer.
- **Avoiding Errors**: Double-check all script components before inscribing to avoid errors that could invalidate the operation.

---

## Conclusion

By adhering to these rules and guidelines, you can ensure that your CAT-20 tokens are managed effectively and securely on the Bitcoin blockchain. Understanding these principles is key to leveraging the full potential of CAT-20, whether you are deploying new tokens, minting additional supply, or transferring tokens between wallets.
