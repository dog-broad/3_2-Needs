# Mining Systems in Blockchain

> ***NOTE: The below text shows the evolution of mining systems in blockchain. If you want the types (PoW, PoS), refer to other notes***

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

> ***NOTE: Still not sure about this answer***  
> *The follwing link showed prommising results: https://www.babypips.com/crypto/learn/what-are-different-types-of-bitcoin-wallets*

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



# Anonymity

Anonymity, particularly in the context of financial transactions like Bitcoin, refers to the ability of users to conduct transactions without revealing their true identity or personal information. It involves masking the link between the real-world identity of the sender or recipient and their transactions on the blockchain, the public ledger that records all Bitcoin transactions.

### Types of Anonymity

1. **Pseudonymity**: Bitcoin transactions are pseudonymous, meaning users interact using pseudonyms or Bitcoin addresses rather than their real names. Each transaction is linked to a Bitcoin address, which is a hash of the public key used to send and receive Bitcoins. Pseudonymity allows users to maintain a level of privacy by not directly associating their real-world identity with their Bitcoin transactions.

2. **Unlinkability**: True anonymity requires unlinkability, meaning that it should be difficult to connect multiple transactions or addresses to the same user over time. This prevents someone from tracing a series of transactions back to a single entity or tracking spending habits across different transactions.

### Challenges to Anonymity in Bitcoin

While Bitcoin offers pseudonymity, several factors challenge its anonymity:

- **Blockchain Transparency**: Bitcoin's blockchain is publicly accessible and transparent. Every transaction, once confirmed, is recorded permanently and can be viewed by anyone. This transparency allows for transaction analysis, which can potentially reveal patterns and links between addresses.

- **Transaction Graph Analysis**: Techniques like transaction graph analysis can exploit the transparency of the blockchain. By analyzing patterns in transaction flows and linking multiple addresses to a single user based on spending habits or identifiable patterns (like change addresses), researchers or adversaries can deanonymize users.

- **Address Reuse**: Reusing Bitcoin addresses can compromise anonymity. If multiple transactions are associated with a single address, it becomes easier to link those transactions together, reducing the unlinkability of the user's activities.

- **IP Address Deanonymization**: When users broadcast transactions to the Bitcoin network, their IP addresses can potentially be exposed. Although techniques like using TOR can mitigate this risk, sophisticated adversaries may still be able to deanonymize transactions by correlating IP addresses with transaction timing and patterns.

### Enhancing Anonymity in Bitcoin

Several methods and technologies aim to enhance anonymity in Bitcoin transactions:

- **Mixing Services**: Mixing or coin tumbling services aim to break the link between the sender and recipient addresses by mixing coins from multiple users. This process makes it harder to trace the origin of specific coins, thus enhancing anonymity.

<div style="text-align:center;"><img src="img/2024-06-23-13-51-30.png" alt="Mixing Services" style="width:350px;height:200px;"></div>

- **Privacy Coins**: Cryptocurrencies like Monero and Zcash incorporate specific features (such as ring signatures and zero-knowledge proofs) to achieve stronger anonymity and privacy guarantees compared to Bitcoin.

- **Improving Practices**: Users can adopt best practices like using new addresses for each transaction, avoiding address reuse, and using technologies like TOR or VPNs to obfuscate their IP addresses when interacting with the Bitcoin network.




# Transaction Verification

Bitcoin transaction verification is a critical process within the Bitcoin network that ensures the validity and integrity of transactions before they are permanently recorded on the blockchain. Here’s a detailed explanation of how Bitcoin transaction verification works:

### Overview of Bitcoin Transactions

Bitcoin transactions involve the transfer of value (Bitcoins) from one address to another. Each transaction is broadcasted to the entire network of nodes (computers running the Bitcoin software) where it awaits validation and inclusion in a block.

### Steps in Bitcoin Transaction Verification

1. **Transaction Propagation**: When a user initiates a Bitcoin transaction, it is broadcasted to all nodes in the network. Nodes collect these transactions in a memory pool (mempool) where they wait to be selected by miners to be included in the next block.

2. **Transaction Validation by Nodes**:
   - **Syntax and Data Structure Check**: Nodes first validate the transaction’s syntax and data structure to ensure it conforms to Bitcoin’s protocol rules. This includes verifying that the transaction format, inputs, outputs, and other details are correctly formatted.
   
   - **Script Validation**: Each transaction includes a script that specifies conditions for spending the Bitcoins (e.g., providing a valid digital signature). Nodes verify that the script executes correctly and that the spender has the necessary private keys to authorize the transaction.

   - **Double Spending Prevention**: Nodes check that the transaction inputs (Bitcoins being spent) have not been spent before in any previous transactions. This prevents double spending, where the same Bitcoins are used in multiple transactions simultaneously.

   - **Transaction Outputs**: Nodes verify that the sum of inputs equals the sum of outputs to ensure there’s no creation or destruction of Bitcoins beyond the specified rules.

3. **Transaction Propagation and Inclusion**: Once a transaction is validated by a node, it propagates it to other nodes in the network. Miners select transactions from the mempool to include in a new block they are mining.

### Role of Miners in Transaction Verification

While nodes perform initial transaction validation, miners play a crucial role in:
- **Block Creation**: Miners collect validated transactions and attempt to create a new block by solving a cryptographic puzzle (Proof of Work).
- **Inclusion in Blockchain**: Once a miner solves the puzzle, they broadcast the new block to the network. Other nodes and miners verify the block and its transactions before adding it to their own copy of the blockchain.
