# Hello world on Renec
This example is forked from Solana

The project comprises of:

* An on-chain hello world program
* A client that can send a "hello" to an account and get back the number of
  times "hello" has been sent

## Translations
- [Traditional Chinese](README_ZH_TW.md)
- [Simplified Chinese](README_ZH_CN.md)

## Table of Contents
- [Hello world on Renec](#hello-world-on-renec)
  - [Table of Contents](#table-of-contents)
  - [Quick Start](#quick-start)
    - [Configure CLI](#configure-cli)
    - [Start local Renec cluster](#start-local-renec-cluster)
    - [Install npm dependencies](#install-npm-dependencies)
    - [Build the on-chain program](#build-the-on-chain-program)
    - [Deploy the on-chain program](#deploy-the-on-chain-program)
    - [Run the JavaScript client](#run-the-javascript-client)
    - [Expected output](#expected-output)
      - [Not seeing the expected output?](#not-seeing-the-expected-output)
    - [Customizing the Program](#customizing-the-program)
  - [Learn about Renec](#learn-about-renec)
  - [Learn about the client](#learn-about-the-client)
    - [Entrypoint](#entrypoint)
    - [Establish a connection to the cluster](#establish-a-connection-to-the-cluster)
    - [Check if the helloworld on-chain program has been deployed](#check-if-the-helloworld-on-chain-program-has-been-deployed)
    - [Send a "Hello" transaction to the on-chain program](#send-a-hello-transaction-to-the-on-chain-program)
    - [Query the Renec account used in the "Hello" transaction](#query-the-renec-account-used-in-the-hello-transaction)
  - [Learn about the on-chain program](#learn-about-the-on-chain-program)
    - [Programming on Renec](#programming-on-renec)
  - [Pointing to a public Renec cluster](#pointing-to-a-public-renec-cluster)
  - [Expand your skills with advanced examples](#expand-your-skills-with-advanced-examples)

## Quick Start

[![Open in
Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/renec-labs/example-helloworld)

If you decide to open in Gitpod then refer to
[README-gitpod.md](README-gitpod.md), otherwise continue reading.

The following dependencies are required to build and run this example, depending
on your OS, they may already be installed:

- Install node (v14 recommended)
- Install npm
- Install Rust v1.56.1 or later from https://rustup.rs/
- Install Renec v1.10.35 or later from
  https://docs.renec.com/cli/install-renec-cli-tools

If this is your first time using Rust, these [Installation
Notes](README-installation-notes.md) might be helpful.

### Configure CLI

> If you're on Windows, it is recommended to use [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to run these commands

1. Set CLI config url to localhost cluster

```bash
renec config set --url http://127.0.0.1:8899
```

2. Create CLI Keypair

If this is your first time using the Renec CLI, you will need to generate a new keypair:

```bash
renec-keygen new
```

### Start local Renec cluster

This example connects to a local Renec cluster by default.

Start a local Renec cluster:
```bash
renec-test-validator
```
> **Note**: You may need to do some [system tuning](https://docs.renec.com/running-validator/validator-start#system-tuning) (and restart your computer) to get the validator to run

Listen to transaction logs:
```bash
renec logs
```

### Install npm dependencies

```bash
npm install
```

### Build the on-chain program

There is both a Rust and C version of the on-chain program, whichever is built
last will be the one used when running the example.

```bash
npm run build:program-rust
```

```bash
npm run build:program-c
```

### Deploy the on-chain program

```bash
renec program deploy dist/program/helloworld.so
```

### Run the JavaScript client

```bash
npm run start
```

### Expected output

Public key values will differ:

```bash
Let's say hello to a Renec account...
Connection to cluster established: http://127.0.0.1:8899 { 'feature-set': 2045430982, 'renec-core': '1.7.8' }
Using account AiT1QgeYaK86Lf9kudqKthQPCWwpG8vFA1bAAioBoF4X containing 0.00141872 RENEC to pay for fees
Using program Dro9uk45fxMcKWGb1eWALujbTssh6DW8mb4x8x3Eq5h6
Creating account 8MBmHtJvxpKdYhdw6yPpedp6X6y2U9dCpdYaZJdmwV3A to say hello to
Saying hello to 8MBmHtJvxpKdYhdw6yPpedp6X6y2U9dCpdYaZJdmwV3A
8MBmHtJvxpKdYhdw6yPpedp6X6y2U9dCpdYaZJdmwV3A has been greeted 1 times
Success
```

#### Not seeing the expected output?

- Ensure you've [started the local cluster](#start-local-renec-cluster),
  [built the on-chain program](#build-the-on-chain-program) and [deployed the program to the cluster](#deploy-the-on-chain-program).
- Inspect the program logs by running `renec logs` to see why the program failed.
  - ```bash
    Transaction executed in slot 5621:
    Signature: 4pya5iyvNfAZj9sVWHzByrxdKB84uA5sCxLceBwr9UyuETX2QwnKg56MgBKWSM4breVRzHmpb1EZQXFPPmJnEtsJ
    Status: Error processing Instruction 0: Program failed to complete
    Log Messages:
      Program G5bbS1ipWzqQhekkiCLn6u7Y1jJdnGK85ceSYLx2kKbA invoke [1]
      Program log: Hello World Rust program entrypoint
      Program G5bbS1ipWzqQhekkiCLn6u7Y1jJdnGK85ceSYLx2kKbA consumed 200000 of 200000 compute units
      Program failed to complete: exceeded maximum number of instructions allowed (200000) at instruction #334
      Program G5bbS1ipWzqQhekkiCLn6u7Y1jJdnGK85ceSYLx2kKbA failed: Program failed to complete

### Customizing the Program

To customize the example, make changes to the files under `/src`.  If you change
any files under `/src/program-rust` or `/src/program-c` you will need to
[rebuild the on-chain program](#build-the-on-chain-program) and [redeploy the program](#deploy-the-on-chain-program).

Now when you rerun `npm run start`, you should see the results of your changes.

## Learn about Renec

More information about how Renec works is available in the [Renec
documentation](https://docs.renec.com/) and all the source code is available on
[github](https://github.com/renec-labs/renec)

Further questions? Visit us on [Discord](https://discordapp.com/invite/pquxPsq)

## Learn about the client

The client in this example is written in TypeScript using:
- [Renec web3.js SDK](https://github.com/renec-labs/renec-web3.js)
- [Renec web3 API](https://renec-labs.github.io/renec-web3.js)

### Entrypoint

The [client's
entrypoint](https://github.com/renec-labs/example-helloworld/blob/ad52dc719cdc96d45ad8e308e8759abf4792b667/src/client/main.ts#L13)
does five things.

### Establish a connection to the cluster

The client establishes a connection with the cluster by calling
[`establishConnection`](https://github.com/renec-labs/example-helloworld/blob/ad52dc719cdc96d45ad8e308e8759abf4792b667/src/client/hello_world.ts#L92).

### Establish an account to pay for transactions

The client ensures there is an account available to pay for transactions,
and creates one if there is not, by calling
[`establishPayer`](https://github.com/renec-labs/example-helloworld/blob/ad52dc719cdc96d45ad8e308e8759abf4792b667/src/client/hello_world.ts#L102).

### Check if the helloworld on-chain program has been deployed

In [`checkProgram`](https://github.com/renec-labs/example-helloworld/blob/ad52dc719cdc96d45ad8e308e8759abf4792b667/src/client/hello_world.ts#L144),
the client loads the keypair of the deployed program from `./dist/program/helloworld-keypair.json` and uses
the public key for the keypair to fetch the program account. If the program doesn't exist, the client halts
with an error. If the program does exist, it will create a new account with the program assigned as its owner
to store program state (number of hello's processed).

### Send a "Hello" transaction to the on-chain program

The client then constructs and sends a "Hello" transaction to the program by
calling
[`sayHello`](https://github.com/renec-labs/example-helloworld/blob/ad52dc719cdc96d45ad8e308e8759abf4792b667/src/client/hello_world.ts#L209).
The transaction contains a single very simple instruction that primarily carries
the public key of the helloworld program account to call and the "greeter"
account to which the client wishes to say "Hello" to.

### Query the Renec account used in the "Hello" transaction

Each time the client says "Hello" to an account, the program increments a
numerical count in the "greeter" account's data.  The client queries the
"greeter" account's data to discover the current number of times the account has
been greeted by calling
[`reportGreetings`](https://github.com/renec-labs/example-helloworld/blob/ad52dc719cdc96d45ad8e308e8759abf4792b667/src/client/hello_world.ts#L226).

## Learn about the on-chain program

The [on-chain helloworld program](/src/program-rust/Cargo.toml) is a Rust program
compiled to [Berkeley Packet Filter
(BPF)](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter) bytecode and stored as an
[Executable and Linkable Format (ELF) shared
object](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format).

The program is written using:
- [Renec Rust SDK](https://github.com/renec-labs/renec/tree/master/sdk)

### Programming on Renec

To learn more about Renec programming model refer to the [Programming Model
Overview](https://docs.renec.com/developing/programming-model/overview).

To learn more about developing programs on Renec refer to the [On-Chain
Programs Overview](https://docs.renec.com/developing/on-chain-programs/overview)

## Pointing to a public Renec cluster

Renec maintains three public clusters:
- `devnet` - Development cluster with airdrops enabled
- `testnet` - Tour De RENEC test cluster without airdrops enabled
- `mainnet-beta` -  Main cluster

Use the Renec CLI to configure which cluster to connect to.

To point to `devnet`:
```bash
renec config set --url devnet
```

To point back to the local cluster:
```bash
renec config set --url http://127.0.0.1:8899
```

## Writing the client in Rust

This example details writing the client code in typescript; however
the Renec client program can be written in any language. For an
example client written in Rust and an accompanying write up see [this
repo](https://github.com/ezekiiel/simple-renec-program).

## Expand your skills with advanced examples

There is lots more to learn; The following examples demonstrate more advanced
features like custom errors, advanced account handling, suggestions for data
serialization, benchmarking, etc...

- [Programming
  Examples](https://github.com/renec-labs/renec-program-library/tree/master/examples)
- [Token
  Program](https://github.com/renec-labs/renec-program-library/tree/master/token)
- [Token Swap
  Program](https://github.com/renec-labs/renec-program-library/tree/master/token-swap)
