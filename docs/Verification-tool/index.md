---
id: verification-tool
title: RNG Authenticity Verification
---

## Introduction

GINAR is a leading company in providing Decentralized Random Number Generation (dRNG) solutions to the iGaming industry. The main focus of whole GINAR, in general, and the focus of this upgrade, in particular, is on providing random numbers with the following characteristics: **unpredictability, public-verifiability, tamper-resistance, transparency**, and **high performance**. Public-verifiability is the property that enables anyone to check the correctness of random number generation from GINAR. We have APIs available to support authenticity verification. This document serves the purpose of explaining how to verify a random number generated by GINAR via an Authenticity Verification API.

If you wish to understand how ginar works in a simple way, please access to this [**Verification Simulator Tool**](https://simulator.ginar.io/#/)


## Authenticity Verification

GINAR provides a UI (called **Authenticity Verification API**) for the sake of making verification intuitively. The verification tool can be found [**HERE**](https://blackbox.ginar.io). At a high level, the verifying procedure shows all the details relating to how a random number is generated. Moreover, this information is written onto the Ethereum blockchain to guarantee that manipulating is impossible. Following is the description of how to use this tool. 

Note that each random beacon will be associated with a **TicketID**. This **TicketID** is sufficient to retrieve all the information relating to how a random number has been produced. 

### 1. Search the TicketID

If the **Gaming/iGaming Providers** already integrated GINAR random service API, then you can simply click on **Verify Ticket** to access the **RNG Authenticity Verification** tool. Else, you can access the **RNG Authenticity Verification** tool [**HERE**](https://blackbox.ginar.io), and enter **TicketID** then click **SEARCH**. 

![Step 1](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/Step%201.png?raw=true)

> **TicketID** - The root of all the RNG generation processes. It contains random information from end users, operators, GINAR and public Ethereum

You can use TicketID to verify beacon value and timestamp when this beacon has been generated. This value will be the root of all calculations for the later generation.


### 2. Verification Results

- If you get a message **The Authenticity of this game can not be verified by GINAR**, that means the **TicketID** has not been initiated yet.

![NotFound](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/TicketNotFound.png?raw=true)

- If you get a message **Verified by GINAR**, that means the **TicketID** has been initiated by GINAR.

![NotFound](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/Verified%20by%20GINAR.png?raw=true)

- If the TicketID is **Verified by GINAR** and **used**, that means the **TicketID** had been initiated and used.

![Found](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/Ticket%20Found.png?raw=true)

- If the **TicketID** is **Verified by GINAR** and **unused**, that means the **TicketID** had been initiated but not yet used.

![Unused](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/StatusUnused.png?raw=true)

> **Requester**: The customer’s name

> **Serial number**: An unique number allocated by GINAR corresponding to a given API key

> **Creator**: The creator of the ticket - **GINAR Decentralized RNG**.

> **Status**: **Used** - The ticket ID has been initiated and used / **Unused** - The ticket ID has been initiated but has not been used

### 3. View Full Detail

If you wish to see the full detail of how the random number has been generated, click **View Full Detail**.

- **Status - Unused** The **ticketID** has been initiated but has not been used

![StatusUnused](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/Status_Unused.png?raw=true)

- **Status - Used** The **ticketID** has been initiated and used

![StatusUsed](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/Status%20Used.png?raw=true)

> **User Data**: the meta-data sent along when requesting random numbers. Click on the hyperlink **Show** to access this meta-data

> **Ethereum Entropy**: an additional input in GINAR’s process obtained from public blockchain every **1 hour**. This information is recorded on the Ethereum and can be accessed via the hyperlink **View on Etherscan**

> **Ethereum Batch of IDs Records**: the Merkel proof for all **ticketID**’s since for each session, GINAR generates concurrently 1024 ticketIDs at the same time. This information is recorded on the Ethereum and can be accessed via the hyperlink **View on Etherscan**

> **Created Timestamp**: The time when ticket being created

> **Numbers of GINAR Contributing Nodes**: the number of eligible nodes contributing to generating the random number

> **Generated Output**: The output random number

> **Used timestamp**: The time when the random number has been used


All of these fields are recorded on the blockchain, click **View block information** to get access to it.

![BlockInfo](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/Blockinfo.png?raw=true)

Click the **Json Data** tab to get the full detail and/or copy it.

![JSON](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/JSON.png?raw=true)

On the **Random Number Generating Process** block, click on **Show eligible contributors** to see the information of each contributor.

![Eligible](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/EligibleNode.png?raw=true)

Each eligible contributor block includes:
> **Public key**: The public key of the GINARATOR

> **Credential**: Proof of correctness of the contribution with respect to the **TicketID**, Serial number and the **Public key**

> **Contribution**: The value contributed by the eligible node (GINARATOR)

> **Signature**: The signature of the GINARATOR on the contribution



If one wishes to verify the **Credential**, click on the hyperlink **VRF tool** to get access to the public **Python** implementation.

![VRF](https://github.com/GINARTeam/docs/blob/master/docs/Verification-tool/VRF.png?raw=true)

This code is implemented and maintained by GINAR and can be run online without the need for installing any software. To verify the credential of a GINARATOR, replace the following values in the code (as shown in the example in the comment section) and click **Run**:
- **TicketID**
- **Serial number**
- **Public key** of the GINARATOR
- **Credential**

If the credential is **correct** (i.e this GINARATOR is eligible, and the contribution has not been manipulated), the rightmost screen will display **"The credential is valid: True"** with some sort of additional information. Otherwise, the output will be **"The credential is valid: False"**.

