## Title
**zkUNO - UNO on chain**

## Project Background
Zero-Knowledge UNO (zkUNO) is a cutting-edge, multiplayer digital adaptation of the classic UNO game. Whether a casual player or a competitive strategist, it offers a revolutionary gaming experience that combines the fun of UNO with the power of blockchain technology.

The game is built in a hybrid mode where the key operations are driven on chain and some of the validation/verification aspects are run off chain. At any given instance the chain has the most recent state of the game recorded. Needless to mention, the key aspects of the game are kept confidential via efficient proofing mechanisms.

This is a multi player real time game therefore, we use websockets to sync hands and decks across clients while ensuring the chain has a record of relevant game actions. We have a prototype of the game built on Kakarot (zkEVM) and deployed on their testnet currently. For better distribution we also have a telegram bot built to play the game from within telegram.

[zkUNO](https://gameofuno.vercel.app/) | [GitHub](https://github.com/ronykris/gameofuno) | [Telegram](https://t.me/zkcard_bot) |[ X (Twitter)](https://x.com/zk_UNO)

## Proposal Overview
Below is a high-level overview and summary of the proposal. 

- **Problem:** 
    Below are few of the glaring problems traditional card game and the infrastructure suffers from and these result in limited adoption as well. To elaborate a bit;
    Traditional online card games suffer from trust issues where players doubt the fairness of the game. 
    Centralized platforms often have control over the game mechanics, leading to potential manipulation or lack of transparency.
     The visibility of players’ hands and decks can compromise the integrity of the game, as some players might gain an unfair advantage.
     Steep learning curve and limited awareness of the blockchain ecosystem restricts infrastructure adoption.

- **Solution:**
    zkUNO will address these concerns by ensuring the game mechanics are decentralized and transparent by deploying on Mina, while the privacy layer guarantees that players' hands and the deck remain hidden. This ensures that no player can gain an unfair advantage, and the integrity of the game is preserved. 
    
    The integration of an efficient proving system further ensures that all moves and deck is verifiable without compromising privacy by building the proofs using O1js.
    
    zkUNO will be a complete re-write of the smart contract and privacy layer. The existing prototype currently has the smart contract written in Solidity and the privacy layer is via a commit and reveal scheme and moves validated on the client. That said, below is a high level summary of the features we plan to implement:
    
    1. **Decentralized Gameplay:** Implement the core game logic, including card shuffling, dealing, and turn management, in O1js. This ensures that all game actions are transparent, verifiable, and tamper-proof.
    2. **Game State Management and Updates:** The state of the game (e.g., current turn, remaining cards, and played cards) to be managed on-chain and synced across all clients via websockets. This will ensure  it is consistent, tamper-proof, and available to all players in real-time. State updates occur with every action taken by players, such as drawing a card or playing a card.
    3. **Action Validation and Application:** Each player’s action is validated off chain in the client and replicated to on-chain. This ensure it adheres to the game rules and invalid actions are rejected, and the game state is updated only when valid actions are applied.
    4. **State Reconstruction and Verification:** To maintain fairness and transparency, the game state can be reconstructed and verified by any participant or observer using the transaction history recorded on the blockchain. This ensures that all players can audit the game at any time.
    5. **Optimistic UI:** Build an optimistic UI that gathers transactions and submits it on chain as one transaction after a certain number of txns have already happened.
    6. **Confidential Hands and Decks:** Use O1js to create proof of  player hands and the remaining deck. This ensures that no player, except the one holding the cards, can view the contents of any hand.
    7. **Game Features:** Implement multiple game rooms, various UNO rules and point system
    8. **Cryptographic Operations:** Cryptographic primitives such as hashing and encryption/decryption are employed to ensure the security and privacy of game data. For example, the deck is shuffled and encrypted and only the relevant cards are decrypted for each player.
    9. **Deck Shuffling and Initial State Generation:** The deck is shuffled in a cryptographically secure manner using O1js ensuring that the order of card is random and unknown to all players. The initial game state is generated with encrypted/hashed decks and distributed in a manner that ensures no information leakage.

- **Impact:** A major reason why people are intimidated to contribute to this technology is it's learning curve. This project will help to create a **reference architecture** for people to fork and build on top it should they choose to. This will improve adoption of the Mina Blockchain. 

    Based on our market study, it appears that it has a pretty huge addressable market. Bringing the game play on chain makes it less intimidating for people to use it thereby reducing the barrier of adoption.
    
    A major cross section of the gaming community resides on telegram. Therefore, we plan on distirbuting this via telegram.  Giving them an in-app inteface to play digitsed UNO will be a huge crowd puller.
    
    Therefore, this dapp has tremendous potential of sky rocketing Mina adoption and transactions.
- **Audience:** 
![Screenshot 2024-09-18 at 2.38.09 AM](https://hackmd.io/_uploads/HkZllOPpA.png)



## Architecture & Design
The card game will be built in a hybrid architecture where the game logic will reside onchain while the actual validation / verification of hands will happen off chain. The state management across clients will be through websockets and peridocally will be synced to the chain. 

The core components of the game are:

**Smart Contract:** The entire game logic (shuffle, card dealing, turn management) will be handled by the smart contract written in O1js. 

**Game State Management:** Each player's turn, remaining cards, and game state transitions will be periodically synced with the chain.

**Privacy Layer:** This module is responsible for generating succinct proofs of the hands and deck and associated cryptographic algorithms.

**State Reconstruction and Verification:** While the private elements are hidden, the state of the game remains verifiable by all players through cryptographic commitments, ensuring fairness without exposing sensitive information.

**Optimistic UI:** A queue, off chain, will keep record of all transactions and at a particular time or trasnaction cadence it will commit a transaction encompassing all the other ones.

**Websockets:** Websocket layer running in the backend will be responsible for syncing the discard pile, hands and dec across clients.

Below is a detailed sequence diagram of the game flow.

![zkUNO-sequence-diagram](https://hackmd.io/_uploads/B1Gyep_pA.png)


**Tech Stack:**
* Frontend: nextJS
* Client sync: websockets
* Smart contract: O1js
* Transaction cache: Redis


- **Vision:** What is your long-term vision for this project if your proposal is funded?
We intend to take this project to the market and onboard users for actual game play and eventually convert this into a startup.
- **Existing Work :** We had created a prototype of UNO on zkEVM earlier. [GitHub](https://github.com/ronykris/gameofuno)
- **Production Timeline :** Soon after we reach a substantial user base we will deploy it on Mainnet.



##  Budget & milestones

- **Deliverables**: 
	* Smart contract to control game play. Few features below:
		* Create game
		* Join game
		* Shuffle Deck
		* Deal hands
		* End game
	* Proving and verifier system to secure hands and deck
	* Backend service to sync hands, discard pile, deck across clients
	* Optimistic client rollup for transactions
	* Frontend integration + telegram bot
	
- **Mid-Point milestones:** 
    * Sometime end of month 2 would be a good time for a mid point check-in.
- **Project Timeline :** 1M - 3M
- **Budget Requested :**  100,000 MINA
- **Budget Breakdown:** 

    **Milestone 1:**
    * Duration: 1M
    * Budget: 40K MINA
    * Deliverables: Implement key infra pieces and frontend integration (40k Mina)
        * Smart contract with game play features
        * 
        * Backend service to sync hands
        * Frontend integration

    **Milestone 2:** 
    * Duration: 1M
    * Budget: 30K MINA
    Implement the game play logic, websockets and front end integration. 
(30k Mina)
Milestone 3: Test and Deploy on testnet/mainnet and onboard Alpha users
(30k Mina)

- **Wallet Address:** MINA Wallet address for funding. Please ensure to use the same wallet used during the **KYC process**.



## Team Info
Below is the dynamics of the team.

-  **Proposer Github**: [GitHub](https://github.com/ronykris/)
- **Proposer Experience**: Experienced in writing proving systems building distributed scalable solutions and/or zkDapps. Also, experienced in writing zk circuits

-  **Team Members**: 

**Ayush Kumar Singh:** A full stack developer with several wins
and two years of experience in the web3 ecosystem. He has won Filecoin track prizes at ethIndia an]d worked in the Mina ecosystem. As a Core Member of the UniDAO program led by Devfolio, he fosters blockchain innovation on his campus by hosting weekly sessions on DeFi, DAOs, IPFS, NFTs, and hands- on projects.
Devfolio: https://devfolio.co/@Ayush4345
GitHub: https://github.com/ayush4345

**Nikhil Shrivas:** Ace designer and frontend developer with
expertise in scaling protocols and managing product. He has 4+ years of web3 experience on chains with marketing and Content. He is an Ambassador at Arbitrum and several crypto exchanges.
GitHub: https://github.com/nshri1609
Linkedin: https://www.linkedin.com/in/nikhilshrivass/



**Saurabh Shetty:** Web3 and blockchain developer relations
professional with 5+ years of experience. Skilled in developer outreach, technical writing, and community management, Director of TPG_Karnataka, Web3 Developer community, Mina Navigator Hackathon Winner.
GitHub: https://github.com/Saurus9290
Linkedin:https://www.linkedin.com/in/saurabhshettyofficial/


-  **Achievements**: 
1) Midnight Virtual Hackathon Winners.
2) EthGlobal's StarkHack 2024 Bounty Winners.



## Risks & Mitigations

- What risks or dependencies do you foresee with building this project ? 
    - We have to run some performance profiling to check the proof creation times during game play.
- What are your migtigations if any?
    - None at the moment
