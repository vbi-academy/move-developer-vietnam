---
id: sp_local_binaries
sidebar_position: 2
title: Install Sui Binaries Locally
---


Each Sui release provides a set of binaries for several operating systems. You can download these binaries from GitHub and use them to install Sui.

# Pros and Cons
1. **Pros:**

- Much faster compared to installing Sui using Cargo. My machine always takes more than 30 minutes to install Sui = Cargo.
- Easy to control versions

2. **Cons (not entirely cons because there are ways to overcome)**

- Cannot be used globally => declare environment variable

# Steps: How to install Binaries locally?

Visit the following link [Releases · MystenLabs/sui (github.com)](https://github.com/MystenLabs/sui/releases) to download the desired Sui version. In this guide, we will install https://github.com/MystenLabs/sui/releases/tag/testnet-v1.25.0.

If you are a WSL user, you need to transfer the zip file from Windows to WSL. Open WSL terminal and enter the command `explorer.exe .`. Now, File Explorer will open with the location being your current working directory on WSL. You just need to copy the file to this folder.

After downloading the zip file in step 2, continue to extract it using the command `tar -xzvf <filename>.tgz`. The result is you will receive two folders, Target and external-crates. We just need to care about the Target folder.   

![An image example how to install sui](/img/SCR-20240517-upls.png)

