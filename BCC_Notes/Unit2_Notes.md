# Mining Systems in Blockchain

***NOTE: The below text shows the evolution of mining systems in blockchain. If you want the types (PoW, PoS), refer to other notes***

Mining is a fundamental process in blockchain networks, particularly in Bitcoin, where it involves the validation of transactions and the addition of these transactions to the blockchain. Miners compete to solve complex mathematical problems, and the first to solve it gets to add a new block to the blockchain and is rewarded with newly created bitcoins and transaction fees.

### 1. CPU Mining

**Description:**  
CPU (Central Processing Unit) mining was the earliest method used to mine Bitcoin. In the initial days of Bitcoin, users could mine using their regular laptop or desktop computers. The mining process involves solving complex mathematical problems using the CPU's processing power.

**Evolution and Challenges:**  
- **Profitability Decline:** CPU mining became unprofitable within just over a year since the introduction of Bitcoin due to increasing difficulty levels and the emergence of more efficient mining methods.
- **Technology Limitation:** CPUs are not optimized for the parallel processing required for efficient mining, making them slow and inefficient compared to newer methods.

### 2. GPU Mining

**Description:**  
GPU (Graphics Processing Unit) mining became popular as miners shifted from CPUs. GPUs, which are typically used for rendering graphics in PCs, proved to be more efficient for mining due to their ability to perform parallel calculations.

**Evolution and Challenges:**  
- **Performance Boost:** GPUs offered faster processing speeds compared to CPUs, especially when programmed using frameworks like OpenCL.
- **Limitations:** Challenges included overheating issues, the need for specialized hardware setups (e.g., multiple GPUs, specialized motherboards), and increased costs due to high demand from both miners and gamers.

### 3. FPGA Mining

**Description:**  
FPGA (Field Programmable Gate Array) mining followed GPU mining. FPGAs are programmable integrated circuits that can be customized to perform specific tasks like mining operations.

**Evolution and Challenges:**  
- **Performance Improvement:** FPGAs provided significant performance gains over GPUs for mining due to their programmability and efficiency.
- **Accessibility Issues:** Programming FPGAs required expertise in Hardware Description Languages (HDLs) like Verilog and VHDL, limiting their widespread adoption.
- **Short Lifespan:** FPGA mining was quickly overshadowed by the introduction of ASICs (Application Specific Integrated Circuits).

### 4. ASIC Mining

**Description:**  
ASICs are specialized hardware designed specifically for mining cryptocurrencies. They are highly efficient in performing the specific hashing algorithms (like SHA-256 for Bitcoin) used in mining.

**Evolution and Challenges:**  
- **High Hash Rates:** ASICs offer extremely high hash rates, making them much more efficient than CPUs, GPUs, and FPGAs.
- **Centralization Concerns:** ASICs have led to mining becoming centralized in the hands of large mining operations due to their cost and energy requirements.
- **Profitability Shift:** Mining with ASICs has made it difficult for individual miners to compete without significant investment in hardware and electricity costs.

### Mining Pools

**Description:**  
Mining pools are collaborative groups where multiple miners combine their computational resources to increase their chances of successfully mining a block. If a block is mined, the reward is distributed among all participants based on their contributed computational power.

**Evolution and Challenges:**  
- **Increased Efficiency:** Mining pools offer a more consistent income stream compared to solo mining.
- **Centralization Risk:** Large mining pools can potentially control a significant portion of the network hash rate, posing risks like the potential for a 51% attack.
- **Profit Distribution Models:** Pools use various models (e.g., Pay Per Share, Proportional) to distribute rewards among participants.



# Bitcoin Script

Bitcoin Script is a fundamental component of the Bitcoin protocol, serving as a scripting language that defines the conditions under which transactions are executed. Here's a detailed exploration of Bitcoin Script, along with an example illustrating its usage in a typical transaction scenario.

### Bitcoin Script Overview

Bitcoin Script is:
- **Stack-Based**: It operates using a stack data structure where operations are performed on a last-in, first-out (LIFO) basis. This makes it efficient and straightforward for handling transactions.
  
- **Forth-Like**: Similar to Forth, a programming language known for its simplicity and stack manipulation capabilities. Bitcoin Script utilizes postfix notation (Reverse Polish Notation, RPN) where operations follow operands, making it concise and predictable.
  
- **Turing Incomplete**: Designed intentionally without certain features like loops to prevent potentially infinite execution scenarios. This enhances security by avoiding the halting problem, ensuring scripts can't stall the Bitcoin network.

### Example: Pay To PubKey Hash (P2PKH) Transaction

Let’s illustrate Bitcoin Script in action through a basic P2PKH transaction:

1. **Scenario Setup**:
   - Alice wants to send 1 Bitcoin (BTC) to Bob.
   - Bob has provided Alice with his Bitcoin address, which is derived from his public key and encoded using Base58Check.

2. **Transaction Process**:
   - **Locking Script (scriptPubKey)**:
     - Alice creates a transaction specifying Bob's Bitcoin address as the recipient (`Bob'sPubKeyHash`). This address is converted into a locking script (`scriptPubKey`) which locks the funds to Bob's address.
     - The locking script typically looks like: `OP_DUP OP_HASH160 <Bob'sPubKeyHash> OP_EQUALVERIFY OP_CHECKSIG`.
     - This script ensures that the transaction output can only be spent by providing a valid signature matching the public key hash (`Bob'sPubKeyHash`).

3. **Transaction Execution**:
   - Alice broadcasts the transaction to the Bitcoin network.
   - Miners validate the transaction, ensuring Alice has sufficient funds and Bob’s locking conditions (`scriptPubKey`) are met.

4. **Unlocking Script (scriptSig)**:
   - When Bob wants to spend the received 1 BTC, he must provide an unlocking script (`scriptSig`) in the transaction input.
   - The unlocking script includes a digital signature created using Bob’s private key and the public key corresponding to `Bob'sPubKeyHash`.
   - The scriptSig typically looks like: `<Bob'sSignature> <Bob'sPublicKey>`.

5. **Transaction Verification**:
   - Miners verify the transaction input by executing both the unlocking script (`scriptSig`) and the locking script (`scriptPubKey`).
   - If the unlocking script provides a valid signature and meets the conditions set by the locking script, the transaction is considered valid.

6. **Transaction Confirmation**:
   - Once confirmed by the network, the 1 BTC is transferred from Alice's UTXO to Bob's, and Bob can now spend these funds in future transactions.



# Bitcoin Wallets

Bitcoin wallets are a secure and convenient way to store and manage Bitcoin transactions. They offer convenience and security, but they also require trust in the service provider's security measures.

Bitcoin wallets can be classified into several types based on how they store and manage private keys, their security features, and accessibility. Here's a detailed classification of Bitcoin wallets:

### 1. Non-deterministic Wallets
- **Description**: Also known as "just a bunch of keys" wallets.
- **Characteristics**:
  - Private keys are randomly generated by the wallet software.
  - Each new key is generated separately as needed.
  - Requires regular backups and secure storage of each key.
- **Example**: Bitcoin Core client wallets before deterministic features were introduced.

### 2. Deterministic Wallets
- **Description**: Wallets where keys are derived from a seed value.
- **Characteristics**:
  - Keys are generated deterministically using a seed (typically a mnemonic phrase).
  - Offers easier backup and recovery of all keys derived from the seed.
  - Improves key management and reduces the risk of key loss.
- **Example**: Wallets following BIP 39 standard, like Electrum and Jaxx.

### 3. Hierarchical Deterministic (HD) Wallets
- **Description**: A type of deterministic wallet that organizes keys in a tree structure.
- **Characteristics**:
  - Uses a single seed to generate a master key from which all subsequent keys are derived.
  - Allows for easy backup and restoration of an entire wallet using the master key.
  - Enhances portability and organization of keys.
- **Example**: Trezor, Ledger wallets, and software wallets like Electrum that support BIP 32 and BIP 44.

### 4. Brain Wallets
- **Description**: Wallets where the private key is derived from a passphrase memorized by the user.
- **Characteristics**:
  - Private key is generated deterministically from the passphrase.
  - Vulnerable to brute-force attacks if the passphrase is weak.
  - Riskier compared to other types of wallets due to potential passphrase vulnerabilities.
- **Example**: Any wallet that supports generating keys from a passphrase entered by the user.

### 5. Paper Wallets
- **Description**: Physical printouts or offline documents containing keys.
- **Characteristics**:
  - Private keys and addresses are printed or written on paper.
  - Requires physical security and careful handling to prevent loss or theft.
  - Often used for long-term storage rather than frequent transactions.
- **Example**: Generated through services like BitcoinPaperWallet.com or BitAddress.org.

### 6. Hardware Wallets
- **Description**: Secure physical devices designed specifically for key storage.
- **Characteristics**:
  - Tamper-resistant hardware provides enhanced security against physical and remote attacks.
  - Private keys never leave the device, ensuring they are not exposed to online threats.
  - Typically used for significant amounts of cryptocurrency due to their high security.
- **Example**: Trezor, Ledger Nano S/X, and other hardware wallets with secure elements.

### 7. Online Wallets
- **Description**: Wallets hosted and accessed via the internet.
- **Characteristics**:
  - Convenient for everyday transactions and accessible from any device with an internet connection.
  - Relies on the security practices of the online service provider.
  - Generally easier to use but potentially less secure compared to hardware wallets.
- **Example**: GreenAddress, Blockchain.info, and other web-based wallet services.

### 8. Mobile Wallets
- **Description**: Wallet applications installed on mobile devices (smartphones, tablets).
- **Characteristics**:
  - Offers mobility and convenience for making payments on the go.
  - Typically includes QR code scanning for easy payment processing.
  - May vary in security based on the app and device security practices.
- **Example**: Blockchain Wallet, Breadwallet (now BRD), Electrum, Jaxx, and other mobile apps.


### Considerations
Choosing the right Bitcoin wallet depends on factors such as security preferences, convenience, and usage scenarios. Hardware wallets are generally recommended for long-term storage due to their robust security features, while mobile and online wallets offer convenience but require trust in the service provider's security measures. Paper wallets provide offline security but require careful handling. Understanding these distinctions helps users make informed decisions based on their specific needs and priorities.