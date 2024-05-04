# Running a Parimutuel Crank

This document outlines the steps to run a parimutuel crank.

## Prerequisites

- Docker installed on your machine.
- Access to a validator node.

## Docker Image

The Docker image for the parimutuel crank is available at: _public.ecr.aws/n7a0e3o7/parimutuelcrank_

## Configuration

You will need to set several environment variables before running the container. These variables are necessary to configure the crank appropriately:

- **PROGRAM_ID**: Identifier for the program, set to `GUhB2ohrfqWspztgCrQpAmeVFBWmnWYhPcZuwY52WWRe`.
- **NETWORK_KEY**: Different keys for different tokens:
  - USDC: `FoCmS48FRyJrx6bozDijaARYAThdUeUGu4rbGKqBegcH`
  - GUAC: `AytZdG74ZJDWuzL7MJw3cFJywYC75uS1eubxvY4D6aQH`
  - BONK: `AARaFgaGwAoZAGqwf8Kn5aqxpZvuDotMMH6HgckJpCC7`
- **VALIDATOR_URL**: URL of the validator node.
- **PAYER_KEYPAIR**: Base58 encoded private key of the payer.

### Optional Configuration

Some additional optional environment variables include:

- **CRANK_PERIOD**: The frequency of crank operation, default is every 5 seconds.
- **SWEEP_FEES**: Set to `true` to enable automatic fee collection.
- **PREFLIGHT_CHECK**: Set to `true` to enable preflight checks before transactions.
- **CONTINUE_ON_ERROR**: Set to `true` to continue operation even if errors occur.

## Running the Container

To run the parimutuel crank, you can use the following Docker command:

```bash
docker run -e PROGRAM_ID='GUhB2ohrfqWspztgCrQpAmeVFBWmnWYhPcZuwY52WWRe' \
           -e NETWORK_KEY='Your_Network_Key' \
           -e VALIDATOR_URL='Your_Validator_URL' \
           -e PAYER_KEYPAIR='Your_Payer_Keypair' \
           -e CRANK_PERIOD=5 \
           -e SWEEP_FEES=true \
           -e PREFLIGHT_CHECK=true \
           -e CONTINUE_ON_ERROR=true \
           public.ecr.aws/n7a0e3o7/parimutuelcrank
```
Replace Your_Network_Key, Your_Validator_URL, and Your_Payer_Keypair with the appropriate values for your setup.

