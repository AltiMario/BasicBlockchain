# Basic Blockchain

Implementation of a basic and private blockchain with REST APIs to expose functionalities

## Proof of concept for storing star coordinates on-chain

1. The application will create a Genesis Block when we run the application.
2. The user will request the application to send a message to be signed using a Wallet and in this way verify the ownership over the wallet address. The message format will be: `<WALLET_ADRESS>:${new Date().getTime().toString().slice(0,-3)}:starRegistry`;
3. Once the user have the message the user can use a Wallet to sign the message.
4. The user will try to submit the Star object for that it will submit: `wallet address`, `message`, `signature` and the `star` object with the star information.
    The Start information will be formed in this format:

    ```json
        "star": {
            "dec": "68° 52' 56.9",
            "ra": "16h 29m 1.0s",
            "story": "Tell me about this star"
            }
    ```

5. The application will verify if the time elapsed from the request ownership (the time is contained in the message) and the time when you submit the star is less than 5 minutes.
6. If everything is okay the star information will be stored in the block and added to the `chain`
7. The application will allow us to retrieve the Star objects belong to an owner (wallet address).

## How to test

1. Run it using the command `node app.js` (Server Listening for port: 8000)

2. To create the Genesis block:
    http://localhost:8000/block/0

3. Make the first request of ownership sending your wallet address:
    http://localhost:8000/requestValidation

4. Sign the message with your Wallet using a bitcoin node or https://cryptotools.net/bitcoin and https://reinproject.org/bitcoin-signature-tool/#sign for the address and signature generation

5. Submit your Star:
    http://localhost:8000/submitstar

6. Retrieve Stars owned by the wallet:
    http://localhost:8000/blocks/<WALLET_ADDRESS>]

7. Validate the full chain:
    http://localhost:8000/blocks/chainValidation
