---
id: sui-basics-about-sui-cli-sui-keytool-offline-signing
title: Sui Keytool Offline Signing
sidebar_label: Offline Signing
sidebar_position: 1
draft: false
hide_title: false
hide_table_of_contents: false
keywords: [offline signing, security, serialization, signature]
description: Learn about offline signing in Sui Keytool and how it enhances security for transactions.
images: 
last_update:
    date: 2024-5-18
    author: Hien Phan
---


It is essential for you to understand the concept of [Offline Signing](https://docs.sui.io/concepts/cryptography/transaction-auth/offline-signing).

Offline signing is a security feature that allows you to sign transactions using a device that is not directly connected to the Sui network. This can also be applied when using a wallet that is implemented in a programming language different from the one used in the Sui key store, thereby eliminating the need to rely on the Sui key store.

To effectively implement offline signing, there are a few critical steps that need to be followed:
* Step 1: The first step involves the serialization of the data that needs to be signed. This process converts the data into a format that can be easily stored and retrieved without the risk of data manipulation.
* Step 2: The next step is to sign the serialized data. This is done by placing the serialized data in a secure location where it can be signed. The signature process involves creating a unique identifier, known as a signature, which is associated with the corresponding public key.
* Step 3: Finally, execute the signed transaction. This step involves submitting the transaction to the network for verification and subsequent execution. It's crucial to ensure that the transaction has been correctly signed to prevent any issues during the execution process.


