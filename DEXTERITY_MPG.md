# Guide to Creating and Running an MPG

This guide provides a comprehensive overview of the steps required to set up and manage a Dexterity MPG.

## Step 1: Create an MPG

1. **Initialize the MPG**
   Use `rust-bots/bootstrap-script` to initialize your MPG. Initially, do not include any products.
   - **Required Parameters**:
     - **Name**: Name of your MPG
     - **Quote Token (Vault Mint)**: E.g., USDC mint address `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`
     - **Authority Key**: Key pair controlling the MPG
     - **Fees/Incentives Program Pubkey**
     - **Risk Engine Program Pubkey**
     - **Instruments Program Pubkey**
     - **Agnostic Orderbook Program Pubkey**
   - **Decentralization**: After setup, change the authority to an inaccessible keypair (e.g., System Program) to enhance decentralization.

## Step 2: Rollover Products

- Execute `rust-bots/cranks/src/bin/rollover.rs` to manage the rollover of products.

## Step 3: Initialize and Update Risk

- **Initialize Risk**: Use `programs/risk-engine/bots/update_risk_engine` for initial risk parameter setup.
- **Update Risk Regularly**: Continue using the same script to update risk parameters periodically, automated to every 10 minutes if needed.

## Step 4: Automation Using Cranks

- Deploy cranks for `consume`, `expiration`, `settle`, `rollover`, `fees`, and `liquidation` on your cloud compute platform and monitor them.
- **Note**: The risk engine update script terminates after execution; schedule it to run at regular intervals.

## Testing the MPG

1. **Unit Tests**
   - Build all programs with `./build.sh`.
   - Navigate into each program's directory (e.g., `programs/dex`) and execute `cargo test-bpf`.

2. **End-to-End Tests**
   - Start by setting up a local validator and bootstrap a local MPG using `./build.sh --launch --bootstrap --bots`.
   - For Python tests, navigate to `client/`, set up with `poetry install`, and run `poetry run python3 -m dexteritysdk.scripts.test`.
   - For TypeScript tests, proceed to `typescript-sdk/dexterity-ts`, install dependencies with `yarn install`, and navigate to `tests/$YOUR_CHOICE` to run `yarn start`.

## Common Operational Issues

- **TX Size Too Big**: If the MPG's ALT is missing or not initialized properly, run the rollover crank with `--do-alt-immediately`.
- **Positions Not Settling**: Verify the consume crank is functioning properly.
- **Missing Covariance**: Run the risk crank for newly initialized products to avoid errors.

## Debugging and Troubleshooting

Various issues may require different approaches, from updating and redeploying programs to manual interventions. Use `rust-bots/control-panel` with the MPG authority keypair for custom commands as necessary.
