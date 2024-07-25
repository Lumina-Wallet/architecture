# Lumina Wallet Architecture

## Regular Wallet Architecture

```mermaid
flowchart LR
    User --> |Opens Lumina Telegram Wallet| App[Telegram Wallet App]
    App --> |Selects 'Create Wallet'| WalletCreation[Wallet Creation]
    WalletCreation --> |Generate BIP39 Mnemonic| BIP39[BIP39 Mnemonic]
    BIP39 --> |Derive Ed25519 Keys| Ed25519[Ed25519 Keys]
    Ed25519 --> |Generate HD Path| HDPath[HD Path]
    HDPath --> |Create Wallet Using Stellar SDK| StellarSDK[Stellar SDK]
    StellarSDK --> Wallet[Wallet]
    Wallet --> |Send/Receive Money| Transactions
    Wallet --> |Recover Private Key/Seed Phrase| Recovery

    subgraph User Flow
        User --> App
        App --> WalletCreation
        WalletCreation --> BIP39
        BIP39 --> Ed25519
        Ed25519 --> HDPath
        HDPath --> StellarSDK
        StellarSDK --> Wallet
        Wallet --> Transactions
        Wallet --> Recovery
    end



